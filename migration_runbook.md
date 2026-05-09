# 📋 Migration Runbook
## iqbaalcloudporto.site → Auto-Healing Cloud Infrastructure Platform

> **Dokumen ini adalah runbook teknis step-by-step** untuk memigrasikan website `iqbaalcloudporto.site`
> dari stack lama (EC2 + Docker + GitHub Actions + Nginx) ke stack baru (K3s + Argo CD + Jenkins + Prometheus).
>
> **Prinsip utama:** Zero downtime migration. Website lama tetap live sampai stack baru 100% verified.

---

## 🗺️ Overview: Stack Lama vs Stack Baru

| Komponen | Stack Lama (Existing) | Stack Baru (Capstone) |
|---|---|---|
| VM | EC2 (manual) | EC2 `t2.micro` via **Terraform** |
| Orchestration | Docker Compose / standalone | **K3s** (Kubernetes) |
| Web Server | Nginx (container) | Nginx via **K8s Deployment** |
| CI/CD | GitHub Actions | **Jenkins** Pipeline |
| GitOps | ❌ | **Argo CD** |
| Config Mgmt | ❌ | **Ansible** (hardening + install) |
| Monitoring | Prometheus + Grafana (manual) | Prometheus + Alertmanager via **Ansible** |
| CDN | Cloudflare | Cloudflare (tetap, tidak berubah) |
| Registry | Docker Hub | Docker Hub (tetap) |

---

## ✅ Pre-Migration Checklist

Sebelum mulai migrasi, pastikan semua item ini sudah terpenuhi:

### Capstone Readiness (Wajib Semua ✅)
- [ ] Pipeline Jenkins Infra berjalan sukses minimal **3x berturut-turut** tanpa error
- [ ] Pipeline Jenkins App berjalan sukses (build → push → update manifest)
- [ ] Argo CD auto-sync berjalan dan cluster state = Git state
- [ ] Self-healing simulation berhasil: pod deleted → recovered < 60 detik
- [ ] Prometheus + Alertmanager aktif dan alert rule berjalan
- [ ] Akses ke app via `NodePort` atau `Ingress` sudah berfungsi di IP EC2 baru

### Backup & Safety
- [ ] Backup Dockerfile dan semua config dari EC2 lama ke local/Git
- [ ] Screenshot atau export Grafana dashboard yang ada (untuk referensi)
- [ ] Catat semua environment variable yang dipakai app (port, API key, dll.)
- [ ] Catat Cloudflare DNS record yang aktif saat ini
- [ ] Pastikan punya akses SSH ke **kedua** EC2 (lama dan baru)

### Free Tier Check
- [ ] Cek AWS billing dashboard — pastikan usage EC2 masih dalam batas 750 jam/bulan
- [ ] Stop EC2 lama selama jam kerja lab untuk hemat Free Tier hours

---

## 📦 Phase 0: Backup & Inventory Stack Lama

### Step 0.1 — Backup Konfigurasi dari EC2 Lama

SSH ke EC2 lama dan ambil semua config:

```bash
# SSH ke EC2 lama
ssh -i ~/.ssh/your-key.pem ubuntu@<OLD_EC2_IP>

# Backup semua file konfigurasi penting
mkdir -p ~/backup-migration

# Backup docker-compose atau config Docker
cp docker-compose.yml ~/backup-migration/ 2>/dev/null || true
cp Dockerfile ~/backup-migration/ 2>/dev/null || true

# Backup config Nginx (jika ada volume mount atau custom config)
docker cp $(docker ps -q -f name=nginx):/etc/nginx/conf.d/default.conf ~/backup-migration/nginx-default.conf 2>/dev/null || true

# Backup environment variables yang dipakai
docker inspect $(docker ps -q) | grep -A 20 '"Env"' > ~/backup-migration/env-vars.txt

# Backup Prometheus config jika ada custom rules
cp prometheus.yml ~/backup-migration/ 2>/dev/null || true

# Tar semua backup
tar -czf migration-backup-$(date +%Y%m%d).tar.gz ~/backup-migration/

# Download ke local machine (jalankan dari local)
scp -i ~/.ssh/your-key.pem ubuntu@<OLD_EC2_IP>:~/migration-backup-*.tar.gz ./
```

### Step 0.2 — Catat Semua Environment Variables

```bash
# Di EC2 lama, list semua container yang running
docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Ports}}"

# Untuk setiap container, catat env vars
docker inspect <container_name> --format='{{range .Config.Env}}{{println .}}{{end}}'
```

Simpan output ini — akan dipakai sebagai referensi saat membuat K8s `Secret` dan `ConfigMap`.

### Step 0.3 — Catat DNS Record Cloudflare

Login ke Cloudflare dashboard dan screenshot/catat:
- **A Record:** `iqbaalcloudporto.site` → `<OLD_EC2_IP>`
- **A Record:** `www.iqbaalcloudporto.site` → `<OLD_EC2_IP>` (jika ada)
- Proxy status (orange cloud = proxied, grey = DNS only)
- TTL value yang diset

---

## 🐳 Phase 1: Containerize App untuk Kubernetes

Stack lama pakai Docker standalone/Compose. Stack baru butuh manifest K8s. Di phase ini kita siapkan semua manifest tanpa menyentuh infra lama.

### Step 1.1 — Buat/Verifikasi Dockerfile App

Pastikan Dockerfile yang ada sudah optimal untuk production:

```dockerfile
# Dockerfile (contoh untuk app Node.js/static site)
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .

# Security: jangan run sebagai root
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 3000
CMD ["node", "server.js"]
```

> **Catatan:** Sesuaikan Dockerfile dengan stack app kamu (Python/Node/Go/static HTML).

### Step 1.2 — Build & Push Image ke Docker Hub dengan Tag Versi

```bash
# Di local machine atau Jenkins
export DOCKER_USERNAME="your-dockerhub-username"
export APP_VERSION="1.0.0"  # Increment ini setiap release

# Build image
docker build -t ${DOCKER_USERNAME}/iqbaal-portfolio:${APP_VERSION} .
docker build -t ${DOCKER_USERNAME}/iqbaal-portfolio:latest .

# Login dan push
docker login
docker push ${DOCKER_USERNAME}/iqbaal-portfolio:${APP_VERSION}
docker push ${DOCKER_USERNAME}/iqbaal-portfolio:latest

# Verifikasi image bisa di-pull
docker pull ${DOCKER_USERNAME}/iqbaal-portfolio:${APP_VERSION}
```

### Step 1.3 — Buat Kubernetes Manifests

Buat folder struktur di Git repo manifest kamu:

```
k8s-manifests/
├── namespace.yaml
├── app/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   └── secret.yaml          # (di-gitignore, manage via Sealed Secrets atau manual)
├── ingress/
│   └── ingress.yaml
└── monitoring/
    └── servicemonitor.yaml
```

**namespace.yaml:**
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: portfolio
  labels:
    app: iqbaal-portfolio
```

**app/configmap.yaml:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: portfolio-config
  namespace: portfolio
data:
  NODE_ENV: "production"
  PORT: "3000"
  # Tambahkan env vars non-sensitif lainnya
```

**app/secret.yaml** *(jangan commit ke Git — apply manual atau pakai Sealed Secrets):*
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: portfolio-secret
  namespace: portfolio
type: Opaque
stringData:
  # Ganti dengan env vars sensitif kamu
  API_KEY: "your-api-key-here"
```

```bash
# Apply secret manual (tidak via Argo CD)
kubectl apply -f app/secret.yaml
```

**app/deployment.yaml:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: portfolio-app
  namespace: portfolio
  labels:
    app: portfolio-app
spec:
  replicas: 2                    # 2 replicas untuk high availability
  selector:
    matchLabels:
      app: portfolio-app
  strategy:
    type: RollingUpdate          # Zero downtime deployment
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 0          # Pastikan selalu ada pod yang running
  template:
    metadata:
      labels:
        app: portfolio-app
    spec:
      containers:
      - name: portfolio
        image: your-dockerhub-username/iqbaal-portfolio:1.0.0   # TAG INI yang di-update Jenkins
        ports:
        - containerPort: 3000
        envFrom:
        - configMapRef:
            name: portfolio-config
        - secretRef:
            name: portfolio-secret
        resources:
          requests:
            memory: "64Mi"
            cpu: "50m"
          limits:
            memory: "128Mi"
            cpu: "200m"
        livenessProbe:           # K8s self-heal: restart container jika tidak respond
          httpGet:
            path: /
            port: 3000
          initialDelaySeconds: 15
          periodSeconds: 20
          failureThreshold: 3
        readinessProbe:          # Tidak kirim traffic kalau container belum siap
          httpGet:
            path: /
            port: 3000
          initialDelaySeconds: 5
          periodSeconds: 10
      restartPolicy: Always
```

**app/service.yaml:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: portfolio-service
  namespace: portfolio
spec:
  selector:
    app: portfolio-app
  type: NodePort               # Gratis, tidak butuh LoadBalancer berbayar
  ports:
  - protocol: TCP
    port: 80
    targetPort: 3000
    nodePort: 30080            # Akses via http://<EC2_IP>:30080
```

**ingress/ingress.yaml** *(opsional, jika pakai Nginx Ingress Controller):*
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: portfolio-ingress
  namespace: portfolio
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - host: iqbaalcloudporto.site
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: portfolio-service
            port:
              number: 80
```

---

## 🔧 Phase 2: Setup Nginx Ingress + Cloudflare di Stack Baru

### Step 2.1 — Install Nginx Ingress Controller di K3s

K3s sudah bundled dengan Traefik sebagai default ingress, tapi kita install Nginx Ingress agar lebih familiar:

```bash
# Install Nginx Ingress Controller via kubectl
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/baremetal/deploy.yaml

# Verifikasi running
kubectl get pods -n ingress-nginx
kubectl get svc -n ingress-nginx

# Catat NodePort yang diassign untuk port 80 dan 443
# Output contoh: ingress-nginx-controller   NodePort   10.x.x.x   <none>   80:31234/TCP,443:31567/TCP
```

### Step 2.2 — Update Security Group EC2 Baru

Di AWS Console atau via Terraform, tambahkan inbound rules:

```hcl
# Tambahkan di Terraform security group resource
ingress {
  from_port   = 30080
  to_port     = 30080
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]   # Port NodePort app
}

ingress {
  from_port   = 80
  to_port     = 80
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]   # HTTP
}

ingress {
  from_port   = 443
  to_port     = 443
  protocol    = "tcp"
  cidr_blocks = ["0.0.0.0/0"]   # HTTPS
}
```

```bash
# Apply perubahan Terraform
terraform plan
terraform apply
```

### Step 2.3 — Test App di IP EC2 Baru (Sebelum DNS Cutover)

```bash
# Test langsung via IP dan NodePort — tanpa menyentuh DNS
curl -v http://<NEW_EC2_IP>:30080

# Atau buka di browser: http://<NEW_EC2_IP>:30080

# Verifikasi pods running
kubectl get pods -n portfolio
kubectl get svc -n portfolio

# Check logs jika ada issue
kubectl logs -n portfolio deployment/portfolio-app --tail=50
```

> ✅ **Gate:** Lanjut ke Phase 3 HANYA jika app sudah respond normal di IP baru.

---

## 🌐 Phase 3: Staging Validation (Subdomain Sementara)

Sebelum cutover DNS utama, test dulu via subdomain agar website lama tetap live.

### Step 3.1 — Tambah A Record Subdomain di Cloudflare

Di Cloudflare Dashboard:
1. Masuk ke domain `iqbaalcloudporto.site`
2. Klik **DNS** → **Add Record**
3. Tambahkan:
   - **Type:** A
   - **Name:** `new` (akan jadi `new.iqbaalcloudporto.site`)
   - **IPv4 address:** `<NEW_EC2_IP>`
   - **Proxy status:** DNS only (grey cloud) dulu
   - **TTL:** 1 menit

### Step 3.2 — Update Ingress untuk Menerima Subdomain Staging

```yaml
# ingress/ingress.yaml — tambahkan host staging
spec:
  rules:
  - host: new.iqbaalcloudporto.site    # Staging host
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: portfolio-service
            port:
              number: 80
  - host: iqbaalcloudporto.site        # Production host (siap saat cutover)
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: portfolio-service
            port:
              number: 80
```

```bash
# Commit ke Git manifest repo → Argo CD auto-sync
git add ingress/ingress.yaml
git commit -m "feat: add staging subdomain for migration validation"
git push

# Tunggu Argo CD sync (biasanya < 3 menit)
# Monitor di Argo CD dashboard
```

### Step 3.3 — Validation Checklist di Staging

Test semua fungsi di `new.iqbaalcloudporto.site`:

```bash
# Test HTTP response
curl -I http://new.iqbaalcloudporto.site
# Expected: HTTP/1.1 200 OK

# Test konten halaman
curl -s http://new.iqbaalcloudporto.site | grep -i "title"

# Test dari berbagai device/browser (manual)
# - Desktop Chrome
# - Mobile Safari
# - Firefox
```

- [ ] Halaman utama load normal
- [ ] Semua asset (CSS, JS, gambar) load tanpa error
- [ ] Tidak ada 404/500 error di logs
- [ ] Response time acceptable (< 3 detik)
- [ ] Monitoring Prometheus mendeteksi pod dan scraping metrics

> ✅ **Gate:** Lanjut ke Phase 4 HANYA jika semua checklist staging passed.

---

## ✂️ Phase 4: DNS Cutover (Zero Downtime)

Ini adalah momen kritis. Eksekusi di luar jam sibuk (malam hari / weekend).

### Step 4.1 — Kurangi TTL DNS Lama (Lakukan 1 Jam Sebelum Cutover)

Di Cloudflare, ubah TTL A record utama ke nilai minimum:
1. Klik A record `iqbaalcloudporto.site` yang mengarah ke IP lama
2. Ubah TTL → **1 menit**
3. Save

Tunggu 1 jam agar TTL lama expire di seluruh DNS resolver.

### Step 4.2 — Eksekusi Cutover

```bash
# Catat waktu mulai cutover
echo "Cutover started at: $(date)"

# Verifikasi sekali lagi app di IP baru masih running
curl -I http://<NEW_EC2_IP>:30080
kubectl get pods -n portfolio
```

Di Cloudflare Dashboard:
1. Edit A record `iqbaalcloudporto.site`
2. Ganti **IPv4 address** dari `<OLD_EC2_IP>` ke `<NEW_EC2_IP>`
3. Aktifkan **Proxy status** → orange cloud (Cloudflare proxied)
4. TTL → Auto
5. Save

### Step 4.3 — Monitor Propagasi DNS

```bash
# Monitor dari terminal (jalankan beberapa kali selama 10-15 menit)
dig iqbaalcloudporto.site +short
# Pastikan sudah return NEW_EC2_IP

# Test HTTP
curl -I https://iqbaalcloudporto.site
# Expected: HTTP/2 200

# Check dari berbagai DNS resolver
nslookup iqbaalcloudporto.site 8.8.8.8    # Google DNS
nslookup iqbaalcloudporto.site 1.1.1.1    # Cloudflare DNS
```

### Step 4.4 — Smoke Test Production

```bash
# Full smoke test setelah DNS propagasi
curl -s -o /dev/null -w "%{http_code}" https://iqbaalcloudporto.site
# Expected: 200

# Check response time
curl -o /dev/null -s -w "Total: %{time_total}s\n" https://iqbaalcloudporto.site

# Monitor pods selama 15 menit setelah cutover
watch kubectl get pods -n portfolio
```

> ✅ **Gate:** Jika semua smoke test passed dan tidak ada error dalam 15 menit → cutover sukses!

---

## 📊 Phase 5: Post-Migration Verification

### Step 5.1 — Verifikasi Monitoring Stack

```bash
# Cek Prometheus scraping metrics dari portfolio pods
kubectl get servicemonitor -n portfolio

# Port-forward Prometheus untuk cek targets
kubectl port-forward -n monitoring svc/prometheus 9090:9090 &
# Buka http://localhost:9090/targets → pastikan portfolio target = UP

# Port-forward Grafana
kubectl port-forward -n monitoring svc/grafana 3000:3000 &
# Buka http://localhost:3000 → import/verifikasi dashboard
```

### Step 5.2 — Simulasi Self-Healing (Validasi Akhir)

```bash
# Hapus semua pods portfolio secara paksa
kubectl delete pods -n portfolio -l app=portfolio-app

# Monitor recovery (harusnya < 30 detik)
watch kubectl get pods -n portfolio

# Verifikasi website tetap accessible selama recovery
# (karena RollingUpdate + 2 replicas, harusnya zero downtime)
while true; do
  STATUS=$(curl -s -o /dev/null -w "%{http_code}" https://iqbaalcloudporto.site)
  echo "$(date): HTTP $STATUS"
  sleep 2
done
```

### Step 5.3 — Checklist Final Post-Migration

- [ ] `https://iqbaalcloudporto.site` accessible dan return 200
- [ ] HTTPS/SSL certificate aktif (Cloudflare)
- [ ] Semua halaman dan asset load normal
- [ ] Prometheus targets semua status UP
- [ ] Alertmanager aktif dan alert rules loaded
- [ ] Argo CD dashboard menunjukkan status **Synced** dan **Healthy**
- [ ] Self-healing test passed
- [ ] Response time sama atau lebih baik dari sebelumnya

---

## 🗑️ Phase 6: Decommission Stack Lama

> ⚠️ **Tunggu minimal 48 jam setelah cutover** sebelum mematikan stack lama. Pastikan tidak ada traffic yang masih masuk ke IP lama.

### Step 6.1 — Verifikasi Tidak Ada Traffic ke IP Lama

```bash
# Di EC2 lama, monitor access log Nginx selama 24-48 jam
docker logs <nginx_container> --tail=100 -f

# Jika log sepi (hanya bot/crawler), aman untuk shutdown
```

### Step 6.2 — Stop Lalu Terminate EC2 Lama

```bash
# Via AWS CLI
# Step 1: Stop dulu (data masih ada, tidak kena charge CPU)
aws ec2 stop-instances --instance-ids <OLD_EC2_INSTANCE_ID>

# Tunggu 24 jam, pastikan aman
# Step 2: Terminate (hapus permanent)
aws ec2 terminate-instances --instance-ids <OLD_EC2_INSTANCE_ID>
```

### Step 6.3 — Hapus Resource Lama yang Tidak Diperlukan

```bash
# Hapus Security Group lama (jika terpisah dari yang baru)
aws ec2 delete-security-group --group-id <OLD_SG_ID>

# Hapus Elastic IP lama jika ada (EIP berbayar jika tidak dipakai)
aws ec2 release-address --allocation-id <ALLOCATION_ID>

# Hapus subdomain staging di Cloudflare (opsional)
# DNS → hapus A record "new.iqbaalcloudporto.site"
```

---

## 🚨 Rollback Plan

Jika ada masalah setelah cutover, rollback ke stack lama dalam < 5 menit:

```bash
# ROLLBACK STEP 1: Pastikan EC2 lama masih running
aws ec2 start-instances --instance-ids <OLD_EC2_INSTANCE_ID>
# Tunggu status = running (~60 detik)

# ROLLBACK STEP 2: Revert DNS di Cloudflare
# Edit A record iqbaalcloudporto.site → ganti kembali ke OLD_EC2_IP
# Karena TTL sudah di-set 1 menit sebelumnya, propagasi cepat

# ROLLBACK STEP 3: Verifikasi
curl -I https://iqbaalcloudporto.site
dig iqbaalcloudporto.site +short   # Harus return OLD_EC2_IP
```

> **Penting:** Jangan terminate EC2 lama sampai kamu yakin 100% stack baru stabil minimal 48 jam.

---

## 📝 Catatan Biaya Free Tier Selama Migrasi

| Periode | Kondisi | Estimasi |
|---|---|---|
| Phase 0–2 (Lab) | 2 EC2 running bersamaan | ~2x lipat penggunaan jam, hemat dengan stop EC2 lama saat lab |
| Phase 3 (Staging) | 2 EC2 running | Stop EC2 lama di luar jam test |
| Phase 4 (Cutover) | 2 EC2 running sementara | Durasi singkat, aman |
| Phase 5–6 (Post) | 1 EC2 running (baru) | Kembali normal Free Tier |

**Tips hemat Free Tier:**
```bash
# Stop EC2 lama saat tidak dibutuhkan (data tetap aman)
aws ec2 stop-instances --instance-ids <OLD_EC2_INSTANCE_ID>

# Start kembali saat butuh referensi
aws ec2 start-instances --instance-ids <OLD_EC2_INSTANCE_ID>
```

---

*Runbook ini adalah bagian dari Capstone Project: Auto-Healing Cloud Infrastructure Platform*
*Portfolio: https://iqbaalcloudporto.site*