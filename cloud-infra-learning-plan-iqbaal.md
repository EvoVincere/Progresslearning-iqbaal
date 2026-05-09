# 🚀 Junior Cloud Infrastructure Engineer


---

> **Training Philosophy:** Kurikulum 10 hari ini dirancang khusus untuk level **Junior Cloud Infrastructure Engineer**. Pendekatan yang digunakan adalah *hands-on practice* dengan porsi 30% teori dan 70% praktik, berfokus pada penyediaan, arsitektur jaringan, dan otomatisasi infrastruktur cloud secara aman.

---
## Notes Portfolio Cloud Infra Existing
Cloud App Deployment on AWS: https://iqbaalcloudporto.site/
Monitoring: http://16.79.31.234:3000/dashboards , lalu pilih yang "Node exporter monitoring"
Stack : AWS EC2 (VM), Terraform (IaC), Docker (containerization), Nginx (Web Server), Github Actions (CI/CD), Prometheus (Monitoring), Grafana (Monitoring), Cloudflare (CDN)

## Architecture
User → Cloudflare → EC2 → Docker → App
└── Monitoring → Prometheus → Grafana

## 📋 Table of Contents

1. [Learning Objectives](#learning-objectives)
2. [Prerequisites & Tools](#prerequisites)
3. [10-Day Curriculum](#10-day-curriculum)
4. [Capstone Project Architecture](#capstone-project)
5. [Learning Resources](#resources)

---

## 🎯 Learning Objectives {#learning-objectives}

Setelah menyelesaikan program 10 hari ini, Anda akan mampu:
- Memahami arsitektur komputasi, jaringan, dan penyimpanan di **AWS** dan **Tencent Cloud**.
- Mengotomatiskan pembuatan (provisioning) infrastruktur cloud menggunakan **Terraform**.
- Mengelola konfigurasi OS dan *server hardening* menggunakan **Ansible**.
- Membangun pipeline **CI/CD** khusus untuk infrastruktur (*Infrastructure CI/CD*) menggunakan **Jenkins**.
- Melakukan *containerization* dengan **Docker** dan administrasi cluster **Kubernetes** dasar (EKS/TKE).
- Menerapkan metodologi *GitOps* untuk manajemen *cluster* menggunakan **Argo CD**.

---

## 🔧 Prerequisites & Tools Setup {#prerequisites}

### 🧠 Entry-Level Knowledge Requirements (Skill Awal):
- **Dasar Linux (System Administration):** Mampu melakukan navigasi CLI (`cd`, `ls`, `grep`), manajemen file, manajemen *user/permission* (`chmod`, `chown`, `sudo`), dan instalasi paket.
- **Jaringan Dasar (Networking):** Memahami konsep subnetting (CIDR), IP Address, DNS, NAT, dan model TCP-IP. Pemahaman tentang *networking* sangat kritikal di ranah Cloud Infra.
- **Logika Pemrograman:** Memiliki pemahaman dasar tentang *scripting* (Bash/Python) dan format data (JSON, YAML, HCL).
- **Target Peserta:** Cocok untuk *Fresh Graduate* IT, SysAdmin, atau Network Engineer yang ingin *switch career* ke ranah Cloud Infrastructure.

### 💻 Spesifikasi Hardware Minimum:
- CPU: 4 Cores (i5/Ryzen 5)
- RAM: 16 GB (Direkomendasikan untuk lab lokal dengan Minikube/Docker)
- Storage: 100 GB SSD
- OS: Ubuntu Linux (direkomendasikan) atau Windows dengan WSL 2.

### Software Stack (Hari 0):
Instal seluruh *tools* berikut sebelum memulai sesi:
- **Git** & Akun GitHub/GitLab
- **Docker Desktop** / Docker Engine
- **AWS CLI** & Akun AWS (Free Tier)
- **Tencent Cloud CLI (tccli)** & Akun Tencent Cloud
- **Terraform** & **Ansible**
- **Minikube** & **kubectl**

---

## 📅 10-Day Curriculum {#10-day-curriculum}

### DAY 1 — Pemahaman & Comparison: AWS vs Tencent Cloud
**Fokus:** Membangun pemahaman mendalam tentang perbandingan fitur, kelebihan, dan kekurangan antara **AWS** dan **Tencent Cloud** sebagai fondasi sebelum hands-on.

#### 📖 Teori & Pemahaman:
- **Global Infrastructure Comparison:**
  - AWS: 33+ Regions, 100+ Availability Zones, *market leader* global sejak 2006.
  - Tencent Cloud: 30+ Regions, fokus kuat di Asia-Pasifik & China Mainland.
- **Core Services Mapping (Fitur Head-to-Head):**

  | Kategori | AWS | Tencent Cloud | Catatan |
  |---|---|---|---|
  | Compute | EC2 | CVM (Cloud Virtual Machine) | Fitur serupa, pricing model berbeda |
  | Object Storage | S3 | COS (Cloud Object Storage) | Keduanya S3-compatible API |
  | Virtual Network | VPC | VPC | Arsitektur mirip, terminologi sedikit beda |
  | IAM | IAM (Identity & Access Management) | CAM (Cloud Access Management) | AWS lebih mature & granular |
  | Container Orchestration | EKS (Elastic Kubernetes Service) | TKE (Tencent Kubernetes Engine) | TKE gratis control plane |
  | Serverless | Lambda | SCF (Serverless Cloud Function) | AWS ekosistem lebih luas |
  | CDN | CloudFront | CDN (Tencent Cloud CDN) | Tencent unggul di Asia coverage |
  | Database | RDS, DynamoDB | TencentDB (MySQL, Redis, MongoDB) | AWS lebih banyak opsi engine |
  | Monitoring | CloudWatch | Cloud Monitor (CM) | Keduanya built-in monitoring |
  | IaC Support | CloudFormation + Terraform | Terraform (Official Provider) | AWS punya native IaC tool |

- **Kelebihan AWS:**
  - 🟢 Ekosistem terbesar & terlengkap (200+ services).
  - 🟢 Komunitas & dokumentasi paling matang di dunia.
  - 🟢 Free Tier yang sangat generous (12 bulan + always free tier).
  - 🟢 Sertifikasi profesional yang diakui industri global (SAA, SAP, DevOps Pro).
  - 🟢 Integrasi third-party tools paling luas (Terraform, Ansible, dsb).

- **Kekurangan AWS:**
  - 🔴 Pricing yang kompleks & bisa *unexpected cost* jika tidak hati-hati.
  - 🔴 *Learning curve* tinggi karena banyaknya layanan.
  - 🔴 Latency tinggi untuk pengguna di China Mainland (butuh region Beijing/Ningxia terpisah).
  - 🔴 Support plan gratis terbatas (Basic Support saja).

- **Kelebihan Tencent Cloud:**
  - 🟢 Pricing lebih kompetitif, terutama untuk region Asia.
  - 🟢 Performa & latency sangat baik di Asia-Pasifik dan China.
  - 🟢 TKE (Kubernetes) control plane gratis — tidak seperti EKS yang charge ~$0.10/jam.
  - 🟢 Integrasi kuat dengan ekosistem Tencent (WeChat, Mini Program, Gaming).
  - 🟢 UI Console yang relatif lebih sederhana untuk pemula.

- **Kekurangan Tencent Cloud:**
  - 🔴 Dokumentasi bahasa Inggris masih belum selengkap AWS.
  - 🔴 Komunitas global lebih kecil, troubleshooting resource terbatas.
  - 🔴 Jumlah managed services lebih sedikit dibanding AWS.
  - 🔴 Sertifikasi belum sepopuler & se-recognized AWS di pasar kerja global.
  - 🔴 Free Tier lebih terbatas dibanding AWS.

#### 🔬 Praktik & Eksplorasi:
  - Eksplorasi **AWS Management Console** dan **Tencent Cloud Console** — bandingkan UX, navigasi, dan layout dashboard.
  - Setup **AWS CLI** dan **Tencent `tccli`** di lokal, verifikasi koneksi ke masing-masing akun.
  - Membuat **IAM User** (AWS) dan **CAM Sub-user** (Tencent Cloud) dengan *least-privilege policy*.
  - Mereview dan melengkapi tabel referensi di bawah dengan insight pribadi.

#### 📊 Referensi: Kapan Memilih AWS vs Tencent Cloud?

  | Use Case | Pilih AWS | Pilih Tencent Cloud | Alasan |
  |---|---|---|---|
  | **Startup Global / SaaS** | ✅ | — | Ekosistem terlengkap, komunitas besar, mudah scaling ke multi-region global |
  | **Pasar China Mainland** | — | ✅ | Compliance regulasi China (ICP License), latency terbaik, integrasi WeChat/Mini Program |
  | **Asia-Pacific Focused App** | — | ✅ | Pricing lebih murah di region Asia, latency rendah ke SEA & East Asia |
  | **Enterprise / Fortune 500** | ✅ | — | Track record terpanjang, compliance framework terlengkap (HIPAA, SOC, PCI-DSS) |
  | **Gaming & Real-time** | — | ✅ | Tencent punya infra gaming terbaik (anti-DDoS, GAAP, GME), pengalaman dari Tencent Games |
  | **Budget-Conscious / Cost Optimization** | — | ✅ | Harga VM & bandwidth umumnya lebih kompetitif, TKE control plane gratis |
  | **Kubernetes (Managed)** | — | ✅ | TKE control plane gratis vs EKS ~$73/bulan per cluster |
  | **Serverless & Event-Driven** | ✅ | — | AWS Lambda paling mature, integrasi event source terluas (API GW, SQS, S3, dll) |
  | **AI/ML Workloads** | ✅ | — | SageMaker ekosistem ML terlengkap, Bedrock untuk GenAI |
  | **Data Analytics / Big Data** | ✅ | — | Redshift, Athena, EMR, Glue — ekosistem data paling lengkap |
  | **Hybrid Cloud (On-Prem + Cloud)** | ✅ | — | AWS Outposts & Direct Connect lebih mature secara global |
  | **Video Streaming / Media** | — | ✅ | Tencent unggul di video processing (VOD, TRTC, live streaming) |
  | **Belajar & Sertifikasi Karir** | ✅ | — | Free Tier generous, sertifikasi AWS diakui global, resource belajar melimpah |
  | **Multi-Cloud Strategy** | ✅ + ✅ | ✅ + ✅ | Gunakan keduanya: AWS untuk global, Tencent untuk Asia/China coverage |

  > **💡 Kesimpulan Praktis:** Tidak ada yang 100% lebih baik. Pilihan bergantung pada *target market*, *budget*, *compliance*, dan *ecosystem* yang dibutuhkan. Seorang Cloud Engineer yang baik harus bisa bekerja di keduanya.

#### 📝 Deliverable Hari 1:
  - Dokumen perbandingan AWS vs Tencent Cloud (minimal 1 halaman).
  - Screenshot akses berhasil ke kedua console.
  - CLI terverifikasi: `aws sts get-caller-identity` dan `tccli cvm DescribeRegions`.

### DAY 2 — Cloud Networking & Security
**Fokus:** Membangun topologi jaringan cloud yang aman.

#### 📖 Teori & Pemahaman:
- **VPC (Virtual Private Cloud):** Jaringan virtual terisolasi di cloud — ibarat "data center virtual" milik kita sendiri di atas infrastruktur cloud provider.
- **Subnet (Public vs Private):** Public Subnet punya akses internet langsung via IGW; Private Subnet butuh NAT Gateway (berbayar).
- **Route Table:** Aturan routing yang menentukan arah lalu lintas jaringan di dalam VPC.
- **Internet Gateway (IGW):** Gerbang yang menghubungkan VPC ke internet publik.
- **Security Group:** Firewall stateful di level instance yang mengontrol traffic masuk (inbound) & keluar (outbound).
- *Catatan Free Tier: Managed NAT Gateway berbayar mahal (~$32/bulan di AWS), kita akan belajar konsepnya namun praktiknya menggunakan pendekatan Free Tier (Public Subnet + Security Group ketat).*

**Komponen VPC & Analoginya:**

| Komponen | Fungsi | Analogi |
|---|---|---|
| **VPC** | Jaringan virtual terisolasi | Gedung kantor dengan jaringan internal sendiri |
| **Subnet** | Segmentasi jaringan di dalam VPC | Lantai/ruangan berbeda di gedung |
| **Route Table** | Aturan routing lalu lintas jaringan | Papan petunjuk arah di gedung |
| **Internet Gateway** | Gerbang keluar/masuk ke internet | Pintu utama gedung ke jalan raya |
| **Security Group** | Firewall virtual per instance | Satpam di setiap ruangan |
| **NAT Gateway** | Akses internet dari Private Subnet (satu arah keluar) | Pintu darurat (keluar saja, tidak bisa masuk) |

**Public Subnet vs Private Subnet:**

```
┌─────────────────────────────────────────────────────────────┐
│  VPC: 10.0.0.0/16 (65,536 IP addresses)                    │
│                                                             │
│  ┌──────────────────────┐   ┌──────────────────────────┐   │
│  │   PUBLIC SUBNET      │   │   PRIVATE SUBNET         │   │
│  │   10.0.1.0/24        │   │   10.0.2.0/24            │   │
│  │                      │   │                          │   │
│  │  ✅ Punya Public IP  │   │  ❌ Tidak ada Public IP  │   │
│  │  ✅ Akses Internet   │   │  ❌ Tidak bisa diakses   │   │
│  │     langsung (IGW)   │   │     dari internet        │   │
│  │                      │   │  ✅ Butuh NAT Gateway    │   │
│  │  Use case:           │   │     untuk akses keluar   │   │
│  │  - Web Server        │   │                          │   │
│  │  - Bastion Host      │   │  Use case:               │   │
│  │  - Load Balancer     │   │  - Database Server       │   │
│  │                      │   │  - Backend/API           │   │
│  └──────────┬───────────┘   │  - Internal Services     │   │
│             │               └──────────────────────────┘   │
│  ┌──────────▼───────────┐                                   │
│  │  Internet Gateway    │◄── Route Table: 0.0.0.0/0 → IGW  │
│  └──────────┬───────────┘                                   │
└─────────────┼───────────────────────────────────────────────┘
              ▼
         🌐 INTERNET
```

> **Pendekatan Free Tier:** Dalam kurikulum ini kita menggunakan **Public Subnet saja** karena NAT Gateway berbayar. Semua instance ditempatkan di Public Subnet dengan **Security Group ketat** sebagai lapisan keamanan utama.

#### 🏗️ Arsitektur VPC Kurikulum (AWS Free Tier):

```
                          🌐 INTERNET
                              │
                 ┌────────────▼────────────┐
                 │    Internet Gateway     │
                 │       (igw-xxx)         │
                 └────────────┬────────────┘
                              │
┌─────────────────────────────┼──────────────────────────────────┐
│  VPC: cloud-infra-vpc                                          │
│  CIDR: 10.0.0.0/16                                             │
│  Region: ap-southeast-1 (Singapore) / us-east-1 (Virginia)    │
│                                                                 │
│  ┌──────────────────────────┼──────────────────────────────┐   │
│  │  PUBLIC SUBNET: cloud-infra-public-subnet               │   │
│  │  CIDR: 10.0.1.0/24 (254 usable IPs)                    │   │
│  │  AZ: ap-southeast-1a                                    │   │
│  │                         │                                │   │
│  │           ┌─────────────▼─────────────┐                 │   │
│  │           │   ROUTE TABLE             │                 │   │
│  │           │   10.0.0.0/16 → local     │                 │   │
│  │           │   0.0.0.0/0  → igw-xxx    │                 │   │
│  │           └─────────────┬─────────────┘                 │   │
│  │                         │                                │   │
│  │    ╔════════════════════╧═══════════════════╗           │   │
│  │    ║     SECURITY GROUP: sg-infra-main      ║           │   │
│  │    ║   (Firewall — detail di bawah)         ║           │   │
│  │    ╚════════════════════╤═══════════════════╝           │   │
│  │                         │                                │   │
│  │    ┌────────────────────▼────────────────────┐          │   │
│  │    │  EC2: t2.micro (Free Tier)              │          │   │
│  │    │  OS: Ubuntu 22.04 LTS                   │          │   │
│  │    │  Private IP: 10.0.1.x                   │          │   │
│  │    │  Public IP: (Auto-assigned)              │          │   │
│  │    │                                         │          │   │
│  │    │  ┌─────────────────────────────────┐    │          │   │
│  │    │  │       K3s Cluster (Day 6+)      │    │          │   │
│  │    │  │                                 │    │          │   │
│  │    │  │  ┌──────────┐ ┌──────────────┐  │    │          │   │
│  │    │  │  │ App Pods │ │ Jenkins Pod  │  │    │          │   │
│  │    │  │  │ (Nginx)  │ │ (:8080)      │  │    │          │   │
│  │    │  │  └──────────┘ └──────────────┘  │    │          │   │
│  │    │  │  ┌──────────┐ ┌──────────────┐  │    │          │   │
│  │    │  │  │ Argo CD  │ │ Monitoring   │  │    │          │   │
│  │    │  │  │ (:8443)  │ │ Stack        │  │    │          │   │
│  │    │  │  └──────────┘ │ Prometheus   │  │    │          │   │
│  │    │  │               │ (:9090)      │  │    │          │   │
│  │    │  │               │ Grafana      │  │    │          │   │
│  │    │  │               │ (:3000)      │  │    │          │   │
│  │    │  │               │ Alertmanager │  │    │          │   │
│  │    │  │               │ (:9093)      │  │    │          │   │
│  │    │  │               │ Node Exporter│  │    │          │   │
│  │    │  │               │ (:9100)      │  │    │          │   │
│  │    │  │               └──────────────┘  │    │          │   │
│  │    │  └─────────────────────────────────┘    │          │   │
│  │    └─────────────────────────────────────────┘          │   │
│  └─────────────────────────────────────────────────────────┘   │
└────────────────────────────────────────────────────────────────┘
```

**Spesifikasi Resource VPC:**

| Resource | Nama | Nilai | Catatan |
|---|---|---|---|
| **VPC** | `cloud-infra-vpc` | CIDR: `10.0.0.0/16` | 65,536 IP, cukup untuk ekspansi |
| **Public Subnet** | `cloud-infra-public-subnet` | CIDR: `10.0.1.0/24` | 254 usable IPs |
| **Internet Gateway** | `cloud-infra-igw` | Attached ke VPC | Gratis |
| **Route Table** | `cloud-infra-rtb-public` | `0.0.0.0/0 → IGW` | Arahkan traffic ke internet |
| **Security Group** | `sg-infra-main` | Detail di bawah | Firewall utama |
| **EC2 Instance** | `cloud-infra-server` | `t2.micro`, Ubuntu 22.04 | Free Tier: 750 jam/bulan |

#### 🔒 Security Group: Detail Konfigurasi

Security Group berfungsi sebagai **firewall virtual stateful** yang mengontrol traffic masuk (inbound) dan keluar (outbound) di level instance.

> ⚠️ **Prinsip Least Privilege:** Jangan pernah membuka `0.0.0.0/0` untuk semua port. Hanya buka port yang dibutuhkan, dan batasi source IP ke IP Anda sendiri.

**📥 Inbound Rules (Traffic Masuk):**

| # | Port | Protocol | Source | Service | Keperluan | Mulai Hari |
|---|---|---|---|---|---|---|
| 1 | **22** | TCP | `YOUR_IP/32` | **SSH** | Remote access ke server. Dibatasi hanya IP Anda untuk mencegah brute-force attack. | Day 2+ |
| 2 | **80** | TCP | `0.0.0.0/0` | **HTTP** | Akses web aplikasi (Nginx). Dibuka publik agar website bisa diakses user. | Day 5+ |
| 3 | **443** | TCP | `0.0.0.0/0` | **HTTPS** | Akses web aplikasi via SSL/TLS. Wajib untuk production-grade. | Day 5+ |
| 4 | **6443** | TCP | `YOUR_IP/32` | **K3s API Server** | Endpoint `kubectl` untuk mengakses cluster K8s. Dibatasi agar cluster tidak bisa dikontrol sembarang orang. | Day 6+ |
| 5 | **8080** | TCP | `YOUR_IP/32` | **Jenkins Web UI** | Dashboard CI/CD Jenkins. Dibatasi karena Jenkins punya akses ke credential infrastruktur. | Day 7+ |
| 6 | **9090** | TCP | `YOUR_IP/32` | **Prometheus** | Dashboard monitoring metrics. Dibatasi karena expose internal metrics server. | Day 6+ |
| 7 | **9093** | TCP | `YOUR_IP/32` | **Alertmanager** | Dashboard alert management. Dibatasi karena bisa mute/silence alerts. | Day 6+ |
| 8 | **9100** | TCP | `10.0.0.0/16` | **Node Exporter** | Metrics collector OS (CPU, RAM, Disk). Hanya diakses internal VPC oleh Prometheus. | Day 6+ |
| 9 | **3000** | TCP | `YOUR_IP/32` | **Grafana** | Dashboard visualisasi monitoring. Dibatasi karena menampilkan data sensitif infra. | Day 6+ |
| 10 | **30000-32767** | TCP | `YOUR_IP/32` | **K8s NodePort** | Range port untuk expose K8s Services via NodePort (alternatif gratis dari LoadBalancer). | Day 6+ |
| 11 | **8443** | TCP | `YOUR_IP/32` | **Argo CD Web UI** | Dashboard GitOps controller. Dibatasi karena bisa trigger deployment ke cluster. | Day 9+ |

> 💡 **`YOUR_IP/32`** = hanya 1 IP address (IP publik Anda). Cek IP Anda di: `curl ifconfig.me`

**📤 Outbound Rules (Traffic Keluar):**

| # | Port | Protocol | Destination | Keperluan |
|---|---|---|---|---|
| 1 | **All Traffic** | All | `0.0.0.0/0` | Server perlu akses keluar untuk: download packages (`apt`), pull Docker images, push ke Docker Hub, clone Git repos, download Terraform providers. |

> **Kenapa Outbound dibuka semua?** Server kita perlu mengakses berbagai external service. Membatasi outbound secara granular terlalu kompleks untuk learning environment. Di production, biasanya pakai Network ACL atau Proxy tambahan.

#### 🔐 Strategi Keamanan Berlapis:

```
                    🌐 INTERNET
                        │
          ┌─────────────▼──────────────┐
  Layer 1 │    Security Group          │  ← Firewall stateful per instance
          │    (Port filtering)        │     Hanya port tertentu terbuka
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
  Layer 2 │    SSH Key-Based Auth      │  ← Hanya key pair yang valid
          │    (No password login)     │     Password auth dimatikan (Day 4)
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
  Layer 3 │    OS Hardening (Ansible)  │  ← Disable root login, auto-update
          │    (Day 4 - Playbook)      │     Fail2ban, UFW internal
          └─────────────┬──────────────┘
                        │
          ┌─────────────▼──────────────┐
  Layer 4 │    Application Auth        │  ← Login credentials per service
          │    Jenkins, Grafana, Argo  │     (username/password per tool)
          └────────────────────────────┘
```

#### 🔄 Alur Network Traffic:

**1. Engineer → SSH ke Server:**
`Laptop (YOUR_IP) → Internet → IGW → SG (port 22 ✅) → EC2`

**2. User → Akses Web Aplikasi:**
`Browser (Any IP) → Internet → IGW → SG (port 80/443 ✅) → Nginx → App Pod`

**3. Engineer → Akses Jenkins Dashboard:**
`Laptop (YOUR_IP) → SG (port 8080 ✅) → Jenkins` | `Hacker (Random IP) → SG (port 8080 ❌ BLOCKED)`

**4. Prometheus → Scrape Node Exporter (Internal):**
`Prometheus (10.0.1.x) → SG (port 9100, source VPC ✅) → Node Exporter`

**5. EC2 → Pull Docker Image (Outbound):**
`EC2 → SG (outbound all ✅) → IGW → Internet → Docker Hub`

#### 📋 Quick Reference — Port Mapping:

```
┌──────────────────────────────────────────────────────────┐
│                EC2 t2.micro (10.0.1.x)                   │
│                                                          │
│  ┌─────────┬──────────────────────┬───────────────────┐  │
│  │  PORT   │  SERVICE             │  AKSES            │  │
│  ├─────────┼──────────────────────┼───────────────────┤  │
│  │  :22    │  SSH (OpenSSH)       │  🔒 YOUR_IP only  │  │
│  │  :80    │  HTTP (Nginx/App)    │  🌐 Public        │  │
│  │  :443   │  HTTPS (Nginx/App)   │  🌐 Public        │  │
│  │  :3000  │  Grafana             │  🔒 YOUR_IP only  │  │
│  │  :6443  │  K3s API Server      │  🔒 YOUR_IP only  │  │
│  │  :8080  │  Jenkins             │  🔒 YOUR_IP only  │  │
│  │  :8443  │  Argo CD             │  🔒 YOUR_IP only  │  │
│  │  :9090  │  Prometheus          │  🔒 YOUR_IP only  │  │
│  │  :9093  │  Alertmanager        │  🔒 YOUR_IP only  │  │
│  │  :9100  │  Node Exporter       │  🔒 VPC only      │  │
│  │  :30000 │  K8s NodePort Range  │  🔒 YOUR_IP only  │  │
│  │  -32767 │                      │                   │  │
│  └─────────┴──────────────────────┴───────────────────┘  │
│                                                          │
│  🔒 = Restricted     🌐 = Public Access                 │
└──────────────────────────────────────────────────────────┘
```

#### 🔬 Praktik:
  - Membuat VPC (`10.0.0.0/16`) dengan Public Subnet (`10.0.1.0/24`).
  - Membuat dan meng-attach Internet Gateway ke VPC.
  - Mengonfigurasi Route Table: `0.0.0.0/0 → IGW`.
  - Mengonfigurasi **Security Group** sesuai tabel inbound rules di atas.
  - Launch EC2 `t2.micro` di Public Subnet, verifikasi SSH berhasil hanya dari IP sendiri.
  - Verifikasi keamanan: pastikan SSH dari IP lain di-*block* (tes via mobile hotspot/VPN).

#### 📝 Deliverable Hari 2:
  - VPC + Public Subnet + IGW + Route Table berhasil dibuat.
  - Security Group dikonfigurasi sesuai tabel (minimal SSH port 22 dibatasi ke IP sendiri).
  - EC2 `t2.micro` berhasil di-launch, SSH terverifikasi.
  - Screenshot Security Group rules (inbound & outbound).

> ⚠️ **Jangan lupa stop EC2** setelah selesai lab agar Free Tier hours tidak habis. Instance running 24/7 = ~720 jam/bulan (kuota Free Tier: 750 jam).

> 💡 **AWS vs Tencent Cloud — terminologi networking hampir identik** (VPC, Subnet, Security Group, Internet Gateway, Route Table). Skill VPC di AWS langsung transferable ke Tencent Cloud.

### DAY 3 — Infrastructure as Code (IaC) with Terraform
**Fokus:** Mengubah penyediaan infrastruktur manual di console menjadi barisan kode.

#### 📖 Teori & Pemahaman:
- **Declarative IaC:** Kita mendeskripsikan *desired state* (kondisi akhir yang diinginkan), Terraform yang menentukan langkah-langkahnya.
- **Provider:** Plugin yang menghubungkan Terraform ke cloud provider (AWS, Tencent Cloud, dll).
- **State File (`terraform.tfstate`):** "Database" Terraform yang mencatat semua resource yang sudah di-deploy. **Jangan pernah edit manual.**
- **Variables & Outputs:** Parameterisasi kode agar reusable dan fleksibel.
- **Remote Backend:** Menyimpan state file di cloud (S3/COS) agar bisa di-share antar tim dan punya *state locking*.

**Keuntungan IaC vs Manual Console:**

| Aspek | Manual (Console) | IaC (Terraform) |
|---|---|---|
| **Kecepatan** | Klik satu-satu, 30+ menit | `terraform apply`, 3 menit |
| **Konsistensi** | Human error, lupa setting | Selalu identik setiap kali |
| **Dokumentasi** | Tidak ada jejak | Kode = dokumentasi hidup |
| **Rollback** | Hapus manual, bikin ulang | `terraform destroy` + `apply` |
| **Kolaborasi** | Tidak bisa review | Git PR + Code Review |
| **Audit Trail** | Cek CloudTrail satu-satu | Git history lengkap |

#### 💰 Best Practice Free Tier & Estimasi Biaya:

| Resource | Free Tier (AWS) | Berbayar | Keputusan Kita |
|---|---|---|---|
| EC2 | `t2.micro` 750 jam/bulan ✅ | `t3.medium`+ | Pakai `t2.micro` |
| VPC + Subnet + IGW | Gratis ✅ | — | Gratis selamanya |
| Security Group | Gratis ✅ | — | Gratis selamanya |
| EBS (Disk) | 30 GB gp2 ✅ | >30 GB | Pakai 20 GB (aman) |
| Elastic IP | Gratis jika attached ✅ | $3.65/bulan jika idle | Attach ke running instance |
| NAT Gateway | ❌ ~$32/bulan | — | **Skip**, pakai Public Subnet |
| EKS (Managed K8s) | ❌ ~$73/bulan | — | **Skip**, pakai K3s di EC2 |
| S3 (State Backend) | 5 GB gratis ✅ | — | Pakai untuk remote state |

> ⚠️ **Total biaya target: $0/bulan** — Semua resource di bawah ini dirancang 100% Free Tier.

#### 📁 Struktur Project Terraform:

```
cloud-infra-terraform/
├── main.tf              # Resource utama (VPC, Subnet, EC2)
├── variables.tf         # Deklarasi variabel
├── outputs.tf           # Output values (IP, DNS, dll)
├── terraform.tfvars     # Nilai variabel (⚠️ jangan commit jika ada secret)
├── providers.tf         # Konfigurasi provider & backend
├── security-groups.tf   # Security Group rules (terpisah agar rapi)
└── .gitignore           # Exclude: .tfstate, .tfvars, .terraform/
```

#### 🔧 Kode Terraform — AWS Free Tier:

**1. `providers.tf` — Provider & Backend:**
```hcl
terraform {
  required_version = ">= 1.5.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }

  # Remote Backend (aktifkan setelah S3 bucket dibuat)
  # backend "s3" {
  #   bucket         = "cloud-infra-tfstate-iqbaal"
  #   key            = "infra/terraform.tfstate"
  #   region         = "ap-southeast-1"
  #   encrypt        = true
  #   dynamodb_table = "terraform-lock"  # Optional: state locking
  # }
}

provider "aws" {
  region = var.aws_region
}
```

**2. `variables.tf` — Variabel Input:**
```hcl
variable "aws_region" {
  description = "AWS Region untuk deploy"
  type        = string
  default     = "ap-southeast-1"  # Singapore (dekat Indonesia)
}

variable "project_name" {
  description = "Nama project untuk tagging"
  type        = string
  default     = "cloud-infra"
}

variable "vpc_cidr" {
  description = "CIDR block untuk VPC"
  type        = string
  default     = "10.0.0.0/16"
}

variable "public_subnet_cidr" {
  description = "CIDR block untuk Public Subnet"
  type        = string
  default     = "10.0.1.0/24"
}

variable "my_ip" {
  description = "IP publik Anda untuk akses SSH (jalankan: curl ifconfig.me)"
  type        = string
  # Isi di terraform.tfvars → my_ip = "xxx.xxx.xxx.xxx/32"
}

variable "instance_type" {
  description = "Tipe EC2 instance"
  type        = string
  default     = "t2.micro"  # Free Tier!
}

variable "key_pair_name" {
  description = "Nama SSH Key Pair yang sudah dibuat di AWS Console"
  type        = string
}
```

**3. `main.tf` — Resource Utama (VPC + Subnet + EC2):**
```hcl
# ============================================================
# DATA SOURCE — AMI Ubuntu 22.04 terbaru
# ============================================================
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]  # Canonical (Ubuntu official)

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
  filter {
    name   = "virtualization-type"
    values = ["hvm"]
  }
}

# ============================================================
# VPC
# ============================================================
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name    = "${var.project_name}-vpc"
    Project = var.project_name
    ManagedBy = "terraform"
  }
}

# ============================================================
# INTERNET GATEWAY
# ============================================================
resource "aws_internet_gateway" "main" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "${var.project_name}-igw"
  }
}

# ============================================================
# PUBLIC SUBNET
# ============================================================
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = var.public_subnet_cidr
  availability_zone       = "${var.aws_region}a"
  map_public_ip_on_launch = true  # Auto-assign Public IP

  tags = {
    Name = "${var.project_name}-public-subnet"
  }
}

# ============================================================
# ROUTE TABLE (Public)
# ============================================================
resource "aws_route_table" "public" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.main.id
  }

  tags = {
    Name = "${var.project_name}-rtb-public"
  }
}

resource "aws_route_table_association" "public" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public.id
}

# ============================================================
# EC2 INSTANCE — K3s Node (Free Tier)
# ============================================================
resource "aws_instance" "k3s_server" {
  ami                    = data.aws_ami.ubuntu.id
  instance_type          = var.instance_type  # t2.micro (Free Tier)
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.main.id]
  key_name               = var.key_pair_name

  root_block_device {
    volume_size = 20   # GB (Free Tier: max 30 GB)
    volume_type = "gp2"
    encrypted   = true
  }

  tags = {
    Name    = "${var.project_name}-k3s-server"
    Role    = "k3s-server"
    Project = var.project_name
  }
}
```

**4. `security-groups.tf` — Firewall Rules (Sesuai Arsitektur Day 2):**
```hcl
resource "aws_security_group" "main" {
  name        = "${var.project_name}-sg"
  description = "Security Group untuk cloud-infra learning stack"
  vpc_id      = aws_vpc.main.id

  tags = {
    Name = "${var.project_name}-sg"
  }
}

# ─── INBOUND RULES ───────────────────────────────────────

# 1. SSH (Port 22) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "ssh" {
  security_group_id = aws_security_group.main.id
  description       = "SSH access from my IP only"
  from_port         = 22
  to_port           = 22
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 2. HTTP (Port 80) — Public
resource "aws_vpc_security_group_ingress_rule" "http" {
  security_group_id = aws_security_group.main.id
  description       = "HTTP web access"
  from_port         = 80
  to_port           = 80
  ip_protocol       = "tcp"
  cidr_ipv4         = "0.0.0.0/0"
}

# 3. HTTPS (Port 443) — Public
resource "aws_vpc_security_group_ingress_rule" "https" {
  security_group_id = aws_security_group.main.id
  description       = "HTTPS web access"
  from_port         = 443
  to_port           = 443
  ip_protocol       = "tcp"
  cidr_ipv4         = "0.0.0.0/0"
}

# 4. K3s API Server (Port 6443) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "k3s_api" {
  security_group_id = aws_security_group.main.id
  description       = "K3s Kubernetes API Server"
  from_port         = 6443
  to_port           = 6443
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 5. Jenkins (Port 8080) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "jenkins" {
  security_group_id = aws_security_group.main.id
  description       = "Jenkins Web UI"
  from_port         = 8080
  to_port           = 8080
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 6. Prometheus (Port 9090) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "prometheus" {
  security_group_id = aws_security_group.main.id
  description       = "Prometheus monitoring dashboard"
  from_port         = 9090
  to_port           = 9090
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 7. Alertmanager (Port 9093) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "alertmanager" {
  security_group_id = aws_security_group.main.id
  description       = "Alertmanager dashboard"
  from_port         = 9093
  to_port           = 9093
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 8. Node Exporter (Port 9100) — Internal VPC only
resource "aws_vpc_security_group_ingress_rule" "node_exporter" {
  security_group_id = aws_security_group.main.id
  description       = "Node Exporter metrics (internal VPC only)"
  from_port         = 9100
  to_port           = 9100
  ip_protocol       = "tcp"
  cidr_ipv4         = var.vpc_cidr  # 10.0.0.0/16
}

# 9. Grafana (Port 3000) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "grafana" {
  security_group_id = aws_security_group.main.id
  description       = "Grafana monitoring dashboard"
  from_port         = 3000
  to_port           = 3000
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 10. K8s NodePort Range (30000-32767) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "nodeport" {
  security_group_id = aws_security_group.main.id
  description       = "Kubernetes NodePort services"
  from_port         = 30000
  to_port           = 32767
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# 11. Argo CD (Port 8443) — Hanya IP Anda
resource "aws_vpc_security_group_ingress_rule" "argocd" {
  security_group_id = aws_security_group.main.id
  description       = "Argo CD GitOps Web UI"
  from_port         = 8443
  to_port           = 8443
  ip_protocol       = "tcp"
  cidr_ipv4         = var.my_ip
}

# ─── OUTBOUND RULE ───────────────────────────────────────

# Semua traffic keluar diizinkan
resource "aws_vpc_security_group_egress_rule" "all_outbound" {
  security_group_id = aws_security_group.main.id
  description       = "Allow all outbound traffic"
  ip_protocol       = "-1"
  cidr_ipv4         = "0.0.0.0/0"
}
```

**5. `outputs.tf` — Output Penting:**
```hcl
output "vpc_id" {
  description = "ID VPC yang dibuat"
  value       = aws_vpc.main.id
}

output "public_subnet_id" {
  description = "ID Public Subnet"
  value       = aws_subnet.public.id
}

output "instance_public_ip" {
  description = "Public IP EC2 (untuk SSH & akses service)"
  value       = aws_instance.k3s_server.public_ip
}

output "instance_private_ip" {
  description = "Private IP EC2 (di dalam VPC)"
  value       = aws_instance.k3s_server.private_ip
}

output "ssh_command" {
  description = "Command SSH ke server"
  value       = "ssh -i ~/.ssh/${var.key_pair_name}.pem ubuntu@${aws_instance.k3s_server.public_ip}"
}

output "security_group_id" {
  description = "ID Security Group"
  value       = aws_security_group.main.id
}
```

**6. `terraform.tfvars` — Nilai Variabel (⚠️ jangan commit!):**
```hcl
# Isi dengan nilai Anda
aws_region    = "ap-southeast-1"
my_ip         = "YOUR_PUBLIC_IP/32"   # Ganti! Cek: curl ifconfig.me
key_pair_name = "cloud-infra-key"     # Nama key pair di AWS Console
project_name  = "cloud-infra"
```

**7. `.gitignore`:**
```
*.tfstate
*.tfstate.backup
.terraform/
.terraform.lock.hcl
terraform.tfvars     # Jangan commit file yang berisi IP/secret
crash.log
```

#### 🚀 Workflow Terraform (Urutan Eksekusi):

```
┌──────────────────────────────────────────────────────────┐
│  1. terraform init      → Download provider plugins      │
│  2. terraform validate  → Cek syntax & konfigurasi       │
│  3. terraform plan      → Preview perubahan (dry-run)    │
│  4. terraform apply     → Eksekusi & buat resource       │
│  5. terraform output    → Lihat hasil (IP address, dll)  │
│  6. terraform destroy   → Hapus semua resource           │
└──────────────────────────────────────────────────────────┘
```

```bash
# Step-by-step commands:
cd cloud-infra-terraform/

terraform init              # Download AWS provider
terraform validate          # Pastikan tidak ada error syntax
terraform plan              # Preview: apa saja yang akan dibuat?
terraform apply             # Buat semua resource (ketik "yes")
terraform output            # Lihat Public IP untuk SSH

# Selesai lab? Hapus semua agar tidak kena charge:
terraform destroy           # Hapus semua resource (ketik "yes")
```

#### 📝 Deliverable Hari 3:
  - Seluruh file Terraform berhasil ditulis & terstruktur rapi.
  - `terraform plan` menunjukkan 7+ resources to create (VPC, Subnet, IGW, Route Table, SG, SG Rules, EC2).
  - `terraform apply` berhasil — EC2 running di Public Subnet.
  - SSH ke EC2 berhasil via IP dari `terraform output`.
  - `terraform destroy` berhasil menghapus semua resource.
  - (Bonus) Remote Backend ke S3 berhasil dikonfigurasi.

### DAY 4 — Configuration Management with Ansible
**Fokus:** Melakukan *hardening* OS dan konfigurasi puluhan server secara otomatis.

#### 📖 Teori & Pemahaman:
- **Push Mechanism:** Ansible menjalankan perintah dari Control Node ke Managed Nodes via SSH — tidak perlu install agent di server target.
- **Control Node:** Laptop/server tempat Ansible dijalankan (lokal Anda).
- **Managed Nodes:** Server target yang akan dikonfigurasi (EC2/CVM dari Day 3).
- **Inventory:** Daftar server target beserta variabelnya.
- **Playbook:** File YAML yang berisi langkah-langkah konfigurasi (disebut *tasks*).
- **Idempotency:** Menjalankan playbook 1x atau 100x hasilnya **sama** — tidak ada duplikasi atau error. Ini kunci utama Ansible.
- **Role:** Cara mengorganisir playbook menjadi komponen reusable.

**Arsitektur Ansible dalam Kurikulum Kita:**

```
┌──────────────────────┐          SSH (port 22)         ┌──────────────────────┐
│   CONTROL NODE       │ ──────────────────────────────► │   MANAGED NODE       │
│   (Laptop Anda)      │                                 │   (EC2 t2.micro)     │
│                      │    Playbook dikirim via SSH      │                      │
│  ┌────────────────┐  │    & dieksekusi di target        │  ┌────────────────┐  │
│  │ ansible.cfg    │  │                                 │  │ Ubuntu 22.04   │  │
│  │ inventory      │  │    Tidak perlu install           │  │ K3s Server     │  │
│  │ playbooks/     │  │    agent di target!              │  │ Docker         │  │
│  │ roles/         │  │                                 │  │ Monitoring     │  │
│  └────────────────┘  │                                 │  └────────────────┘  │
└──────────────────────┘                                 └──────────────────────┘
```

#### 📁 Struktur Project Ansible:

```
cloud-infra-ansible/
├── ansible.cfg                    # Konfigurasi global Ansible
├── inventory/
│   ├── hosts.ini                  # Inventory statis (manual)
│   └── terraform_inventory.py    # Inventory dinamis (dari Terraform output)
├── playbooks/
│   ├── 01-system-update.yml       # Update & upgrade OS
│   ├── 02-ssh-hardening.yml       # Hardening SSH (disable root, password)
│   ├── 03-install-docker.yml      # Install Docker Engine
│   ├── 04-install-k3s.yml         # Install K3s (Lightweight K8s)
│   ├── 05-install-monitoring.yml  # Install Node Exporter + Prometheus
│   └── site.yml                   # Master playbook (jalankan semua)
├── roles/                         # (Optional) Ansible Roles
└── files/
    ├── sshd_config                # Template konfigurasi SSH
    └── daemon.json                # Template konfigurasi Docker
```

#### 🔧 Konfigurasi & Kode Ansible:

**1. `ansible.cfg` — Konfigurasi Global:**
```ini
[defaults]
# Lokasi inventory file
inventory = inventory/hosts.ini

# SSH user default (Ubuntu AMI = ubuntu)
remote_user = ubuntu

# Lokasi SSH private key
private_key_file = ~/.ssh/cloud-infra-key.pem

# Jangan cek host key (lab only, TIDAK untuk production!)
host_key_checking = False

# Timeout koneksi SSH
timeout = 30

# Tampilkan output yang rapi
stdout_callback = yaml

# Jumlah server yang diproses paralel
forks = 5

[privilege_escalation]
# Otomatis pakai sudo untuk semua task
become = True
become_method = sudo
become_user = root
```

**2. `inventory/hosts.ini` — Inventory Statis:**
```ini
# ============================================================
# Cloud Infrastructure Inventory
# Ganti IP dengan output dari: terraform output instance_public_ip
# ============================================================

[k3s_server]
# Server utama K3s (dari Terraform Day 3)
cloud-infra-server ansible_host=YOUR_EC2_PUBLIC_IP

[k3s_server:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/cloud-infra-key.pem

# ============================================================
# Group: Semua server
# ============================================================
[all:vars]
ansible_python_interpreter=/usr/bin/python3
```

> 💡 **Tip:** Ganti `YOUR_EC2_PUBLIC_IP` dengan IP dari `terraform output instance_public_ip` (Day 3).

**3. `playbooks/01-system-update.yml` — Update & Upgrade OS:**
```yaml
---
# ============================================================
# Playbook: System Update & Upgrade
# Fungsi: Update semua packages OS ke versi terbaru
# ============================================================
- name: System Update & Essential Packages
  hosts: k3s_server
  become: true

  tasks:
    - name: Update apt cache
      ansible.builtin.apt:
        update_cache: yes
        cache_valid_time: 3600  # Cache valid 1 jam

    - name: Upgrade semua packages
      ansible.builtin.apt:
        upgrade: dist
        autoremove: yes
      register: upgrade_result

    - name: Install essential packages
      ansible.builtin.apt:
        name:
          - curl
          - wget
          - vim
          - htop
          - net-tools
          - unzip
          - jq               # JSON processor (berguna untuk K8s)
          - ca-certificates
          - gnupg
          - lsb-release
          - ufw              # Firewall (tambahan di level OS)
          - fail2ban          # Proteksi brute-force SSH
        state: present

    - name: Set timezone ke Asia/Jakarta
      ansible.builtin.timezone:
        name: Asia/Jakarta

    - name: Tampilkan hasil upgrade
      ansible.builtin.debug:
        msg: "System update selesai. Changed: {{ upgrade_result.changed }}"
```

**4. `playbooks/02-ssh-hardening.yml` — Hardening SSH:**
```yaml
---
# ============================================================
# Playbook: SSH Hardening
# Fungsi: Mengamankan akses SSH sesuai best practice
# ============================================================
- name: SSH Security Hardening
  hosts: k3s_server
  become: true

  tasks:
    # ── Disable root login via SSH ──
    - name: Disable root login
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PermitRootLogin'
        line: 'PermitRootLogin no'
        validate: 'sshd -t -f %s'

    # ── Disable password authentication ──
    - name: Disable password authentication
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PasswordAuthentication'
        line: 'PasswordAuthentication no'
        validate: 'sshd -t -f %s'

    # ── Hanya izinkan key-based auth ──
    - name: Enable PubkeyAuthentication
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PubkeyAuthentication'
        line: 'PubkeyAuthentication yes'
        validate: 'sshd -t -f %s'

    # ── Batasi max percobaan login ──
    - name: Set MaxAuthTries to 3
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?MaxAuthTries'
        line: 'MaxAuthTries 3'
        validate: 'sshd -t -f %s'

    # ── Disable empty passwords ──
    - name: Disable empty passwords
      ansible.builtin.lineinfile:
        path: /etc/ssh/sshd_config
        regexp: '^#?PermitEmptyPasswords'
        line: 'PermitEmptyPasswords no'
        validate: 'sshd -t -f %s'

    # ── Restart SSH service ──
    - name: Restart SSH daemon
      ansible.builtin.systemd:
        name: sshd
        state: restarted
        enabled: yes

    # ── Konfigurasi Fail2Ban ──
    - name: Konfigurasi Fail2Ban untuk SSH
      ansible.builtin.copy:
        dest: /etc/fail2ban/jail.local
        content: |
          [sshd]
          enabled = true
          port = 22
          filter = sshd
          logpath = /var/log/auth.log
          maxretry = 5
          bantime = 3600
          findtime = 600
        mode: '0644'

    - name: Enable dan start Fail2Ban
      ansible.builtin.systemd:
        name: fail2ban
        state: restarted
        enabled: yes

    - name: Verifikasi SSH config valid
      ansible.builtin.command: sshd -t
      changed_when: false

    - name: Tampilkan status hardening
      ansible.builtin.debug:
        msg: |
          ✅ SSH Hardening selesai:
          - Root login: DISABLED
          - Password auth: DISABLED
          - Key-based auth: ENABLED
          - Max auth tries: 3
          - Fail2Ban: ACTIVE (ban setelah 5x gagal)
```

**5. `playbooks/03-install-docker.yml` — Install Docker:**
```yaml
---
# ============================================================
# Playbook: Install Docker Engine
# Fungsi: Install Docker dari official repo (bukan snap)
# ============================================================
- name: Install Docker Engine
  hosts: k3s_server
  become: true

  tasks:
    - name: Hapus Docker versi lama (jika ada)
      ansible.builtin.apt:
        name:
          - docker
          - docker-engine
          - docker.io
          - containerd
          - runc
        state: absent

    - name: Tambahkan Docker GPG key
      ansible.builtin.apt_key:
        url: https://download.docker.com/linux/ubuntu/gpg
        state: present

    - name: Tambahkan Docker repository
      ansible.builtin.apt_repository:
        repo: "deb [arch=amd64] https://download.docker.com/linux/ubuntu {{ ansible_distribution_release }} stable"
        state: present
        filename: docker

    - name: Install Docker Engine
      ansible.builtin.apt:
        name:
          - docker-ce
          - docker-ce-cli
          - containerd.io
          - docker-compose-plugin
        state: present
        update_cache: yes

    - name: Tambahkan user ubuntu ke group docker
      ansible.builtin.user:
        name: ubuntu
        groups: docker
        append: yes

    - name: Enable dan start Docker
      ansible.builtin.systemd:
        name: docker
        state: started
        enabled: yes

    - name: Verifikasi Docker terinstall
      ansible.builtin.command: docker --version
      register: docker_version
      changed_when: false

    - name: Tampilkan versi Docker
      ansible.builtin.debug:
        msg: "{{ docker_version.stdout }}"
```

**6. `playbooks/04-install-k3s.yml` — Install K3s (Lightweight K8s):**
```yaml
---
# ============================================================
# Playbook: Install K3s (Lightweight Kubernetes)
# Fungsi: Setup single-node K3s cluster di EC2 Free Tier
# K3s dipilih karena ringan (<512 MB RAM) vs K8s penuh (~2 GB)
# ============================================================
- name: Install K3s Kubernetes Cluster
  hosts: k3s_server
  become: true

  tasks:
    - name: Download dan install K3s
      ansible.builtin.shell: |
        curl -sfL https://get.k3s.io | sh -s - \
          --write-kubeconfig-mode 644 \
          --disable traefik \
          --node-name cloud-infra-node
      args:
        creates: /usr/local/bin/k3s  # Idempotent: skip jika sudah ada

    - name: Tunggu K3s ready (max 60 detik)
      ansible.builtin.command: k3s kubectl get nodes
      register: k3s_nodes
      until: k3s_nodes.rc == 0
      retries: 12
      delay: 5
      changed_when: false

    - name: Buat symlink kubectl
      ansible.builtin.file:
        src: /usr/local/bin/k3s
        dest: /usr/local/bin/kubectl
        state: link
        force: yes

    - name: Copy kubeconfig untuk user ubuntu
      ansible.builtin.copy:
        src: /etc/rancher/k3s/k3s.yaml
        dest: /home/ubuntu/.kube/config
        remote_src: yes
        owner: ubuntu
        group: ubuntu
        mode: '0644'

    - name: Buat direktori .kube
      ansible.builtin.file:
        path: /home/ubuntu/.kube
        state: directory
        owner: ubuntu
        group: ubuntu
        mode: '0755'

    - name: Tampilkan status K3s cluster
      ansible.builtin.command: k3s kubectl get nodes -o wide
      register: k3s_status
      changed_when: false

    - name: Tampilkan node status
      ansible.builtin.debug:
        msg: "{{ k3s_status.stdout_lines }}"
```

**7. `playbooks/05-install-monitoring.yml` — Install Monitoring Stack:**
```yaml
---
# ============================================================
# Playbook: Install Monitoring (Node Exporter)
# Fungsi: Install Prometheus Node Exporter untuk collect
#         metrics OS (CPU, RAM, Disk, Network)
# ============================================================
- name: Install Monitoring - Node Exporter
  hosts: k3s_server
  become: true

  vars:
    node_exporter_version: "1.7.0"

  tasks:
    - name: Buat user system untuk node_exporter
      ansible.builtin.user:
        name: node_exporter
        system: yes
        shell: /usr/sbin/nologin
        create_home: no

    - name: Download Node Exporter
      ansible.builtin.get_url:
        url: "https://github.com/prometheus/node_exporter/releases/download/v{{ node_exporter_version }}/node_exporter-{{ node_exporter_version }}.linux-amd64.tar.gz"
        dest: /tmp/node_exporter.tar.gz

    - name: Extract Node Exporter
      ansible.builtin.unarchive:
        src: /tmp/node_exporter.tar.gz
        dest: /tmp/
        remote_src: yes

    - name: Copy binary ke /usr/local/bin
      ansible.builtin.copy:
        src: "/tmp/node_exporter-{{ node_exporter_version }}.linux-amd64/node_exporter"
        dest: /usr/local/bin/node_exporter
        remote_src: yes
        mode: '0755'
        owner: node_exporter
        group: node_exporter

    - name: Buat systemd service file
      ansible.builtin.copy:
        dest: /etc/systemd/system/node_exporter.service
        content: |
          [Unit]
          Description=Prometheus Node Exporter
          After=network-online.target

          [Service]
          User=node_exporter
          Group=node_exporter
          Type=simple
          ExecStart=/usr/local/bin/node_exporter \
            --web.listen-address=:9100

          [Install]
          WantedBy=multi-user.target
        mode: '0644'

    - name: Reload systemd daemon
      ansible.builtin.systemd:
        daemon_reload: yes

    - name: Enable dan start Node Exporter
      ansible.builtin.systemd:
        name: node_exporter
        state: started
        enabled: yes

    - name: Verifikasi Node Exporter berjalan
      ansible.builtin.uri:
        url: http://localhost:9100/metrics
        return_content: no
        status_code: 200
      register: exporter_check

    - name: Tampilkan status
      ansible.builtin.debug:
        msg: "✅ Node Exporter berjalan di :9100 — Status: {{ exporter_check.status }}"
```

**8. `playbooks/site.yml` — Master Playbook (Jalankan Semua):**
```yaml
---
# ============================================================
# Master Playbook: Jalankan semua konfigurasi secara berurutan
# Usage: ansible-playbook playbooks/site.yml
# ============================================================
- name: "=== STEP 1: System Update & Essential Packages ==="
  import_playbook: 01-system-update.yml

- name: "=== STEP 2: SSH Security Hardening ==="
  import_playbook: 02-ssh-hardening.yml

- name: "=== STEP 3: Install Docker Engine ==="
  import_playbook: 03-install-docker.yml

- name: "=== STEP 4: Install K3s Cluster ==="
  import_playbook: 04-install-k3s.yml

- name: "=== STEP 5: Install Monitoring Stack ==="
  import_playbook: 05-install-monitoring.yml
```

#### 🚀 Workflow Eksekusi Ansible:

```bash
cd cloud-infra-ansible/

# 1. Test koneksi ke server (ping)
ansible k3s_server -m ping

# 2. Jalankan playbook satu-satu (recommended untuk belajar)
ansible-playbook playbooks/01-system-update.yml
ansible-playbook playbooks/02-ssh-hardening.yml
ansible-playbook playbooks/03-install-docker.yml
ansible-playbook playbooks/04-install-k3s.yml
ansible-playbook playbooks/05-install-monitoring.yml

# 3. ATAU jalankan semua sekaligus via master playbook
ansible-playbook playbooks/site.yml

# 4. Cek mode (dry-run) — lihat apa yang akan berubah tanpa eksekusi
ansible-playbook playbooks/site.yml --check

# 5. Jalankan hanya task tertentu (by tag)
ansible-playbook playbooks/site.yml --tags "ssh"

# 6. Lihat fakta server (info OS, RAM, disk, dll)
ansible k3s_server -m setup | head -50
```

#### ✅ Verifikasi Setelah Eksekusi:

```bash
# SSH ke server dan verifikasi:
ssh -i ~/.ssh/cloud-infra-key.pem ubuntu@YOUR_EC2_IP

# Cek Docker
docker --version
docker ps

# Cek K3s / Kubernetes
kubectl get nodes
kubectl get pods -A     # Lihat semua pods system

# Cek Node Exporter
curl http://localhost:9100/metrics | head -20

# Cek Fail2Ban
sudo fail2ban-client status sshd

# Cek SSH config
sudo sshd -T | grep -E "permitrootlogin|passwordauthentication"
# Expected: permitrootlogin no, passwordauthentication no
```

#### 📝 Deliverable Hari 4:
  - `ansible ping` berhasil ke semua server target.
  - Playbook `01-system-update.yml` berhasil — OS ter-update.
  - Playbook `02-ssh-hardening.yml` berhasil — root login & password disabled, Fail2Ban active.
  - Playbook `03-install-docker.yml` berhasil — Docker terinstall & running.
  - Playbook `04-install-k3s.yml` berhasil — K3s cluster running, `kubectl get nodes` = Ready.
  - Playbook `05-install-monitoring.yml` berhasil — Node Exporter active di `:9100`.
  - Jalankan `site.yml` kedua kali → verifikasi **idempotency** (semua task = `ok`, bukan `changed`).

> 💡 **Idempotency Test:** Jalankan `ansible-playbook playbooks/site.yml` dua kali berturut-turut. Eksekusi kedua seharusnya menampilkan `changed=0` — artinya Ansible tahu semua sudah terkonfigurasi dan tidak mengubah apapun. Ini yang membedakan Ansible dari bash script biasa.

### DAY 5 — Containerization with Docker
**Fokus:** Mengemas aplikasi ke dalam container image, persiapan untuk K8s deployment & CI/CD pipeline.

> 💡 **Kenapa Docker masih dibutuhkan padahal K3s pakai containerd?**
> K3s menggunakan `containerd` sebagai *container runtime* (untuk **menjalankan** container). Tapi kita tetap butuh Docker untuk **mem-build image** (`docker build`) dan **push ke registry** (`docker push`). Di Day 7-8, Jenkins pipeline akan melakukan `docker build → push → deploy ke K3s`.

```
┌─────────────────────────────────────────────────────────────────┐
│                    DOCKER vs CONTAINERD                         │
│                                                                 │
│   DOCKER (Day 5)                  CONTAINERD (K3s - Day 6)     │
│   ┌─────────────────┐           ┌─────────────────────────┐   │
│   │ docker build     │           │ crictl (debug only)      │   │
│   │ docker push      │  image   │                          │   │
│   │ docker run       │ ──────►  │ K3s pulls image from     │   │
│   │ docker tag       │  push    │ Docker Hub & runs via    │   │
│   │ Dockerfile       │  to      │ containerd               │   │
│   │                  │ registry │                          │   │
│   └─────────────────┘           └─────────────────────────┘   │
│                                                                 │
│   Untuk: BUILD & PUSH image       Untuk: RUN container di K8s │
└─────────────────────────────────────────────────────────────────┘
```

#### 📖 Teori & Pemahaman:
- **Container vs VM:** Container berbagi kernel OS host (ringan, start dalam detik), VM punya OS sendiri (berat, start dalam menit).
- **Docker Image:** Template read-only yang berisi aplikasi + semua dependensi-nya.
- **Docker Container:** Instance yang running dari sebuah image.
- **Dockerfile:** "Resep" untuk membuat Docker image — setiap instruksi menjadi satu *layer*.
- **Container Registry:** Tempat penyimpanan image (Docker Hub, AWS ECR, dll).
- **Multi-stage Build:** Teknik untuk menghasilkan image yang kecil & aman (build di stage 1, copy hasil ke stage 2).

**Arsitektur Docker:**

```
┌──────────────────────────────────────────────────────┐
│  DOCKER ENGINE (di EC2 t2.micro)                     │
│                                                      │
│  ┌──────────┐   docker build   ┌──────────────────┐ │
│  │Dockerfile│ ───────────────► │  Docker Image     │ │
│  │(source)  │                  │  (read-only)      │ │
│  └──────────┘                  └────────┬─────────┘ │
│                                         │           │
│                              docker run │           │
│                                         ▼           │
│                                ┌────────────────┐   │
│                                │  Container     │   │
│                                │  (running)     │   │
│                                └────────────────┘   │
│                                                      │
│  docker push ──────────►  Docker Hub (Registry)     │
└──────────────────────────────────────────────────────┘
```

#### 🔧 Praktik — Dockerfile & Build:

**1. Contoh Dockerfile — Aplikasi Nginx (Simple):**
```dockerfile
# ============================================================
# Dockerfile: Static Web Application
# Base image: Nginx Alpine (ringan, ~5 MB)
# ============================================================
FROM nginx:alpine

# Metadata
LABEL maintainer="iqbaal"
LABEL description="Cloud Infra Portfolio Web App"

# Copy file web ke Nginx default directory
COPY ./src/ /usr/share/nginx/html/

# Custom Nginx config (optional)
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Health check
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1

# Nginx sudah otomatis start, tidak perlu CMD
```

**2. Contoh Dockerfile — Multi-Stage Build (Best Practice):**
```dockerfile
# ============================================================
# Multi-Stage Build: Build stage + Production stage
# Hasil image jauh lebih kecil & aman (tidak ada build tools)
# ============================================================

# ── STAGE 1: Build ──
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

# ── STAGE 2: Production ──
FROM nginx:alpine AS production
# Copy HANYA hasil build (bukan source code & node_modules)
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
HEALTHCHECK --interval=30s --timeout=3s \
  CMD curl -f http://localhost/ || exit 1
```

> 💡 **Kenapa Multi-Stage?** Stage 1 bisa 500 MB+ (Node.js + dependencies). Stage 2 hanya ~25 MB (Nginx + file HTML/JS hasil build). Image kecil = pull lebih cepat = deploy lebih cepat.

**3. Struktur Project Docker:**
```
cloud-infra-app/
├── Dockerfile
├── .dockerignore          # File yang tidak di-copy ke image
├── docker-compose.yml     # (Optional) untuk local dev
├── nginx.conf             # Custom Nginx config
└── src/
    ├── index.html
    ├── styles.css
    └── app.js
```

**4. `.dockerignore` — Exclude file yang tidak perlu:**
```
.git
.gitignore
node_modules
*.md
.env
.terraform
*.tfstate
```

#### 🚀 Workflow Docker — Build, Test, Push:

```bash
# ── SSH ke EC2 terlebih dahulu ──
ssh -i ~/.ssh/cloud-infra-key.pem ubuntu@YOUR_EC2_IP

# ── 1. Build image ──
docker build -t cloud-infra-app:v1.0 .

# ── 2. Lihat image yang sudah dibuat ──
docker images
# REPOSITORY        TAG     SIZE
# cloud-infra-app   v1.0    25MB

# ── 3. Jalankan container (test lokal) ──
docker run -d --name test-app -p 8888:80 cloud-infra-app:v1.0

# ── 4. Test akses ──
curl http://localhost:8888
# Atau buka browser: http://YOUR_EC2_IP:8888

# ── 5. Lihat logs container ──
docker logs test-app

# ── 6. Masuk ke dalam container (debug) ──
docker exec -it test-app /bin/sh

# ── 7. Stop & hapus container test ──
docker stop test-app && docker rm test-app
```

#### 📦 Push ke Docker Hub:

```bash
# ── 1. Login ke Docker Hub ──
docker login -u YOUR_DOCKERHUB_USERNAME

# ── 2. Tag image sesuai format Docker Hub ──
# Format: docker.io/<username>/<repo>:<tag>
docker tag cloud-infra-app:v1.0 YOUR_DOCKERHUB_USERNAME/cloud-infra-app:v1.0
docker tag cloud-infra-app:v1.0 YOUR_DOCKERHUB_USERNAME/cloud-infra-app:latest

# ── 3. Push ke Docker Hub ──
docker push YOUR_DOCKERHUB_USERNAME/cloud-infra-app:v1.0
docker push YOUR_DOCKERHUB_USERNAME/cloud-infra-app:latest

# ── 4. Verifikasi di Docker Hub ──
# Buka: https://hub.docker.com/r/YOUR_DOCKERHUB_USERNAME/cloud-infra-app
```

> ⚠️ **Docker Hub Free:** Unlimited public repositories, 1 private repo. Untuk learning, public repo cukup.

#### 🔍 Troubleshooting Docker:

```bash
# Container tidak mau start?
docker logs <container_name>          # Lihat error logs
docker inspect <container_name>       # Detail konfigurasi

# Image terlalu besar?
docker history <image_name>           # Lihat size per layer
# → Gunakan multi-stage build & alpine base image

# Port conflict?
docker ps                             # Lihat port yang sudah dipakai
netstat -tlnp | grep <port>           # Cek proses yang pakai port

# Bersihkan resource Docker yang tidak terpakai
docker system prune -a                # Hapus semua unused images & containers
docker volume prune                   # Hapus unused volumes
```

#### 📝 Deliverable Hari 5:
  - Dockerfile berhasil ditulis (minimal versi simple Nginx).
  - `docker build` berhasil — image terbuat tanpa error.
  - `docker run` berhasil — aplikasi bisa diakses via browser/curl.
  - Docker Hub account dibuat & `docker push` berhasil.
  - Image bisa dilihat di Docker Hub web dashboard.
  - (Bonus) Multi-stage Dockerfile berhasil — bandingkan size vs single-stage.

> 💡 **Koneksi ke Day 7:** Image yang di-push ke Docker Hub hari ini akan menjadi output dari Jenkins CI pipeline di Day 7. Jenkins akan otomatis `docker build → push` setiap ada code change.

### DAY 6 — K3s Cluster Administration & Application Deployment
**Fokus:** Mengelola cluster K3s dan men-deploy aplikasi pertama ke Kubernetes.

> 💡 **Kenapa K3s, bukan K8s (EKS/TKE)?**
> EKS = ~$73/bulan, TKE = control plane gratis tapi worker node berbayar. K3s = **100% gratis**, ringan (<512 MB RAM), dan compatible dengan semua API Kubernetes. Cocok untuk learning & single-node cluster di Free Tier.

#### 📖 Teori & Pemahaman:

**K3s vs K8s (Full Kubernetes):**

| Aspek | K8s (Full) | K3s (Lightweight) |
|---|---|---|
| **RAM Minimum** | ~2 GB | ~512 MB ✅ |
| **Binary Size** | 1+ GB (multiple components) | ~60 MB (single binary) ✅ |
| **Install** | Kompleks (kubeadm, multi-step) | 1 command ✅ |
| **Container Runtime** | Docker / containerd / CRI-O | containerd (built-in) ✅ |
| **Storage Backend** | etcd (butuh cluster 3 node) | SQLite (single node) ✅ |
| **K8s API Compatible** | ✅ | ✅ (100% compatible) |
| **Cocok untuk** | Production enterprise | Edge, IoT, Learning, Dev ✅ |

**Arsitektur K3s Single-Node (Setup Kita):**

```
┌─────────────────────────────────────────────────────────┐
│  EC2 t2.micro (K3s Single Node)                         │
│                                                         │
│  ┌───────────────────────────────────────────────────┐  │
│  │  K3s Server (Control Plane + Worker)              │  │
│  │                                                   │  │
│  │  ┌─────────────┐  ┌───────────────────────────┐   │  │
│  │  │ API Server  │  │  Scheduler + Controller   │   │  │
│  │  │ (:6443)     │  │  Manager                  │   │  │
│  │  └─────────────┘  └───────────────────────────┘   │  │
│  │                                                   │  │
│  │  ┌─────────────┐  ┌───────────────────────────┐   │  │
│  │  │ SQLite      │  │  Kubelet + Kube-proxy     │   │  │
│  │  │ (etcd       │  │  (Worker components)      │   │  │
│  │  │  pengganti) │  │                           │   │  │
│  │  └─────────────┘  └───────────────────────────┘   │  │
│  │                                                   │  │
│  │  ┌─────────────────────────────────────────────┐  │  │
│  │  │  PODS (Container workloads)                 │  │  │
│  │  │                                             │  │  │
│  │  │  ┌─────────┐ ┌──────────┐ ┌─────────────┐  │  │  │
│  │  │  │ App Pod │ │ Monitor  │ │ Argo CD     │  │  │  │
│  │  │  │ (Nginx) │ │ Pod      │ │ Pod         │  │  │  │
│  │  │  └─────────┘ └──────────┘ └─────────────┘  │  │  │
│  │  └─────────────────────────────────────────────┘  │  │
│  └───────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

**Konsep Kubernetes yang Wajib Dipahami:**

| Konsep | Penjelasan | Analogi |
|---|---|---|
| **Pod** | Unit terkecil di K8s, berisi 1+ container | 1 kontainer pengiriman |
| **Deployment** | Mengatur jumlah replika Pod & rolling update | Manajer pabrik |
| **Service** | Expose Pod ke jaringan (internal/external) | Nomor telepon kantor |
| **Namespace** | Isolasi logis di dalam cluster | Departemen di perusahaan |
| **NodePort** | Expose service ke port di node (30000-32767) | Pintu masuk dari luar |
| **ConfigMap** | Konfigurasi external (key-value) | File setting |
| **Secret** | Data sensitif (password, token) — encoded | Brankas |

#### 🔬 Praktik — Verifikasi K3s Cluster:

> K3s sudah ter-install via Ansible Playbook `04-install-k3s.yml` di Day 4. Hari ini fokus ke **administrasi & deployment**.

```bash
# SSH ke EC2
ssh -i ~/.ssh/cloud-infra-key.pem ubuntu@YOUR_EC2_IP

# ── Verifikasi cluster ──
kubectl get nodes
# NAME                STATUS   ROLES                  AGE   VERSION
# cloud-infra-node    Ready    control-plane,master   1d    v1.28.x+k3s1

kubectl cluster-info
kubectl get pods -A              # Semua pods di semua namespace
kubectl top nodes                # Resource usage (CPU/RAM)
```

#### 📦 Deploy Aplikasi Pertama — Nginx via K8s Manifest:

**1. `k8s-manifests/namespace.yml` — Buat Namespace:**
```yaml
# ============================================================
# Namespace: Isolasi logis untuk aplikasi kita
# ============================================================
apiVersion: v1
kind: Namespace
metadata:
  name: cloud-infra
  labels:
    project: cloud-infra
    environment: learning
```

**2. `k8s-manifests/deployment.yml` — Deploy Nginx:**
```yaml
# ============================================================
# Deployment: Menjalankan 2 replika Nginx Pod
# Jika 1 pod mati, K8s otomatis buat yang baru (self-healing)
# ============================================================
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-app
  namespace: cloud-infra
  labels:
    app: nginx-app
spec:
  replicas: 2                    # Jumlah pod yang running
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
        - name: nginx
          image: nginx:alpine    # Image ringan (~5 MB)
          ports:
            - containerPort: 80
          resources:
            requests:
              memory: "32Mi"     # Minimum RAM
              cpu: "50m"         # Minimum CPU (0.05 core)
            limits:
              memory: "64Mi"     # Maximum RAM
              cpu: "100m"        # Maximum CPU (0.1 core)
          livenessProbe:         # K8s cek apakah pod masih hidup
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 5
            periodSeconds: 10
          readinessProbe:        # K8s cek apakah pod siap terima traffic
            httpGet:
              path: /
              port: 80
            initialDelaySeconds: 3
            periodSeconds: 5
```

**3. `k8s-manifests/service.yml` — Expose via NodePort:**
```yaml
# ============================================================
# Service: Expose Nginx ke luar cluster via NodePort
# NodePort = alternatif gratis dari LoadBalancer (yang berbayar)
# ============================================================
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
  namespace: cloud-infra
  labels:
    app: nginx-app
spec:
  type: NodePort               # Expose ke port di node
  selector:
    app: nginx-app             # Pilih pods dengan label ini
  ports:
    - protocol: TCP
      port: 80                 # Port internal service
      targetPort: 80           # Port di container
      nodePort: 30080          # Port yang bisa diakses dari luar
                               # Akses: http://EC2_PUBLIC_IP:30080
```

#### 🚀 Deploy & Verifikasi:

```bash
# ── 1. Apply semua manifest ──
kubectl apply -f k8s-manifests/namespace.yml
kubectl apply -f k8s-manifests/deployment.yml
kubectl apply -f k8s-manifests/service.yml

# Atau apply semua sekaligus:
kubectl apply -f k8s-manifests/

# ── 2. Verifikasi deployment ──
kubectl get all -n cloud-infra
# NAME                             READY   STATUS    RESTARTS   AGE
# pod/nginx-app-xxx-yyy            1/1     Running   0          30s
# pod/nginx-app-xxx-zzz            1/1     Running   0          30s
#
# NAME                    TYPE       CLUSTER-IP    PORT(S)        AGE
# service/nginx-service   NodePort   10.43.x.x     80:30080/TCP   30s
#
# NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
# deployment.apps/nginx-app   2/2     2            2           30s

# ── 3. Test akses dari lokal ──
curl http://localhost:30080         # Dari dalam EC2
# Atau dari browser: http://YOUR_EC2_IP:30080

# ── 4. Lihat detail pod ──
kubectl describe pod -n cloud-infra -l app=nginx-app
kubectl logs -n cloud-infra -l app=nginx-app --tail=20
```

#### 🔄 Simulasi Self-Healing:

```bash
# ── Hapus satu pod secara manual ──
kubectl delete pod -n cloud-infra -l app=nginx-app --field-selector=metadata.name=$(kubectl get pods -n cloud-infra -o jsonpath='{.items[0].metadata.name}')

# ── Lihat K8s otomatis membuat pod pengganti ──
kubectl get pods -n cloud-infra -w   # -w = watch (real-time)
# Pod baru akan muncul dalam hitungan detik!

# ── Verifikasi tetap 2 replika ──
kubectl get deployment -n cloud-infra
# nginx-app   2/2     2            2           5m
```

#### 📊 Deploy Monitoring Stack ke K3s (Prometheus + Grafana):

**`k8s-manifests/monitoring-namespace.yml`:**
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: monitoring
```

**`k8s-manifests/prometheus-config.yml` — Prometheus ConfigMap:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: prometheus-config
  namespace: monitoring
data:
  prometheus.yml: |
    global:
      scrape_interval: 15s
      evaluation_interval: 15s

    scrape_configs:
      # Scrape Prometheus sendiri
      - job_name: 'prometheus'
        static_configs:
          - targets: ['localhost:9090']

      # Scrape Node Exporter (sudah install di Day 4)
      - job_name: 'node-exporter'
        static_configs:
          - targets: ['HOST_IP:9100']
            labels:
              instance: 'cloud-infra-server'

      # Scrape K8s pods (auto-discovery)
      - job_name: 'kubernetes-pods'
        kubernetes_sd_configs:
          - role: pod
        relabel_configs:
          - source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
            action: keep
            regex: true
```

**`k8s-manifests/prometheus-deployment.yml`:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: prometheus
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: prometheus
  template:
    metadata:
      labels:
        app: prometheus
    spec:
      containers:
        - name: prometheus
          image: prom/prometheus:latest
          ports:
            - containerPort: 9090
          args:
            - '--config.file=/etc/prometheus/prometheus.yml'
            - '--storage.tsdb.retention.time=7d'
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"
          volumeMounts:
            - name: config
              mountPath: /etc/prometheus
      volumes:
        - name: config
          configMap:
            name: prometheus-config
---
apiVersion: v1
kind: Service
metadata:
  name: prometheus-service
  namespace: monitoring
spec:
  type: NodePort
  selector:
    app: prometheus
  ports:
    - port: 9090
      targetPort: 9090
      nodePort: 30090       # Akses: http://EC2_IP:30090
```

**`k8s-manifests/grafana-deployment.yml`:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000
          env:
            - name: GF_SECURITY_ADMIN_PASSWORD
              value: "admin123"    # Ganti di production!
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "200m"
---
apiVersion: v1
kind: Service
metadata:
  name: grafana-service
  namespace: monitoring
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 30030       # Akses: http://EC2_IP:30030
```

**Deploy Monitoring:**
```bash
kubectl apply -f k8s-manifests/monitoring-namespace.yml
kubectl apply -f k8s-manifests/prometheus-config.yml
kubectl apply -f k8s-manifests/prometheus-deployment.yml
kubectl apply -f k8s-manifests/grafana-deployment.yml

# Verifikasi
kubectl get all -n monitoring
# Akses Prometheus: http://YOUR_EC2_IP:30090
# Akses Grafana:    http://YOUR_EC2_IP:30030 (admin / admin123)
```

#### 🛠️ Kubectl Cheatsheet (Perintah Admin Penting):

```bash
# ── Cluster Info ──
kubectl cluster-info                      # Info cluster
kubectl get nodes -o wide                 # Status node detail
kubectl top nodes                         # CPU/RAM usage node
kubectl top pods -A                       # CPU/RAM usage semua pods

# ── Namespace ──
kubectl get namespaces                    # List semua namespace
kubectl config set-context --current --namespace=cloud-infra  # Set default ns

# ── Pod Management ──
kubectl get pods -A                       # Semua pods, semua namespace
kubectl describe pod <name> -n <ns>       # Detail pod (events, errors)
kubectl logs <pod-name> -n <ns> -f        # Stream logs real-time
kubectl exec -it <pod-name> -n <ns> -- /bin/sh  # Masuk ke pod

# ── Deployment ──
kubectl scale deployment nginx-app -n cloud-infra --replicas=3  # Scale up
kubectl rollout status deployment/nginx-app -n cloud-infra       # Status rollout
kubectl rollout undo deployment/nginx-app -n cloud-infra         # Rollback

# ── Debug ──
kubectl get events -n cloud-infra --sort-by='.lastTimestamp'     # Events
kubectl get pods -n cloud-infra -o wide                          # Pod + Node info
```

#### 📝 Deliverable Hari 6:
  - K3s cluster ter-verifikasi: `kubectl get nodes` = Ready.
  - Namespace `cloud-infra` berhasil dibuat.
  - Nginx Deployment (2 replika) berhasil running.
  - Service NodePort berhasil — Nginx diakses via `http://EC2_IP:30080`.
  - Self-healing test berhasil — pod dihapus → pod baru otomatis muncul.
  - Prometheus berhasil deploy di `:30090`, Grafana di `:30030`.
  - (Bonus) Grafana dashboard menampilkan metrics dari Node Exporter.

### DAY 7 — Continuous Integration (CI) with Jenkins
**Fokus:** Membangun server otomatisasi (CI) untuk mem-build Docker image & push ke registry secara otomatis.

#### 📖 Teori & Pemahaman:
- **Continuous Integration (CI):** Praktik otomatisasi build & test setiap kali ada code change di Git repository.
- **Jenkins:** Server otomatisasi open-source yang paling populer — self-hosted, gratis, dan sangat extensible.
- **Jenkinsfile:** File deklaratif yang mendefinisikan pipeline CI/CD sebagai kode (*Pipeline as Code*).
- **Declarative Pipeline:** Syntax Jenkinsfile yang terstruktur dengan `pipeline { stages { stage { steps {} } } }`.

**Arsitektur Jenkins dalam Kurikulum Kita:**

```
┌──────────────────────────────────────────────────────────────┐
│  EC2 t2.micro (K3s Cluster)                                  │
│                                                              │
│  ┌────────────────────────────────────────────────────────┐  │
│  │  Jenkins Pod (Docker-in-Docker)                        │  │
│  │                                                        │  │
│  │  ┌──────────────┐    ┌─────────────────────────────┐   │  │
│  │  │ Jenkins UI   │    │  Pipeline Execution         │   │  │
│  │  │ (:8080)      │    │                             │   │  │
│  │  └──────────────┘    │  1. Git Checkout            │   │  │
│  │                      │  2. Lint Dockerfile          │   │  │
│  │                      │  3. Docker Build             │   │  │
│  │                      │  4. Docker Push → Hub        │   │  │
│  │                      │  5. Update K8s Manifest      │   │  │
│  │                      └─────────────────────────────┘   │  │
│  └────────────────────────────────────────────────────────┘  │
│                           │                                   │
│                           │ docker push                       │
│                           ▼                                   │
│                    Docker Hub (Registry)                       │
└──────────────────────────────────────────────────────────────┘
         ▲
         │ Webhook / Poll SCM
         │
    GitHub Repository
```

#### 🔧 Opsi 1: Install Jenkins via Docker (Langsung di EC2)

> Opsi ini paling simpel — jalankan Jenkins sebagai Docker container langsung di EC2.

```bash
# SSH ke EC2
ssh -i ~/.ssh/cloud-infra-key.pem ubuntu@YOUR_EC2_IP

# ── 1. Buat volume untuk persist data Jenkins ──
docker volume create jenkins_home

# ── 2. Jalankan Jenkins container ──
docker run -d \
  --name jenkins \
  --restart=unless-stopped \
  -p 8080:8080 \
  -p 50000:50000 \
  -v jenkins_home:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v /usr/bin/docker:/usr/bin/docker \
  --user root \
  jenkins/jenkins:lts

# ── 3. Ambil initial admin password ──
docker logs jenkins 2>&1 | grep -A 2 "initialAdminPassword"
# ATAU:
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword

# ── 4. Akses Jenkins Web UI ──
# Buka browser: http://YOUR_EC2_IP:8080
# Masukkan initial password → Install suggested plugins → Create admin user
```

> ⚠️ **Docker Socket Mount:** `-v /var/run/docker.sock:/var/run/docker.sock` memungkinkan Jenkins menjalankan `docker build` & `docker push` dari dalam container-nya (Docker-in-Docker pattern).

#### 🔧 Opsi 2: Deploy Jenkins ke K3s (Kubernetes-native)

**`k8s-manifests/jenkins-deployment.yml`:**
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: cicd
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: jenkins-pvc
  namespace: cicd
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins
  namespace: cicd
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      securityContext:
        fsGroup: 1000
      containers:
        - name: jenkins
          image: jenkins/jenkins:lts
          ports:
            - containerPort: 8080
              name: web
            - containerPort: 50000
              name: agent
          resources:
            requests:
              memory: "256Mi"
              cpu: "200m"
            limits:
              memory: "512Mi"
              cpu: "500m"
          volumeMounts:
            - name: jenkins-data
              mountPath: /var/jenkins_home
      volumes:
        - name: jenkins-data
          persistentVolumeClaim:
            claimName: jenkins-pvc
---
apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: cicd
spec:
  type: NodePort
  selector:
    app: jenkins
  ports:
    - name: web
      port: 8080
      targetPort: 8080
      nodePort: 30080       # Akses: http://EC2_IP:30080
    - name: agent
      port: 50000
      targetPort: 50000
```

```bash
# Deploy Jenkins ke K3s
kubectl apply -f k8s-manifests/jenkins-deployment.yml

# Tunggu pod ready
kubectl get pods -n cicd -w

# Ambil initial password
kubectl exec -n cicd $(kubectl get pods -n cicd -l app=jenkins -o jsonpath='{.items[0].metadata.name}') -- cat /var/jenkins_home/secrets/initialAdminPassword

# Akses: http://YOUR_EC2_IP:30080
```

#### ⚙️ Setup Jenkins — Plugin & Credentials:

**Plugin yang perlu diinstall** (Manage Jenkins → Plugins → Available):
1. **Docker Pipeline** — untuk build Docker image di pipeline
2. **Git** — integrasi dengan Git repository
3. **Pipeline** — Jenkinsfile support (biasanya sudah terinstall)
4. **Credentials Binding** — manage secrets/credentials

**Credentials yang perlu ditambahkan** (Manage Jenkins → Credentials → Global):

| ID Credential | Type | Isi | Keperluan |
|---|---|---|---|
| `dockerhub-creds` | Username with Password | Docker Hub username & password | Push image ke Docker Hub |
| `github-token` | Secret text | GitHub Personal Access Token | Clone private repo & update manifest |

```
Manage Jenkins → Credentials → System → Global credentials → Add Credentials
  Kind: Username with password
  ID: dockerhub-creds
  Username: YOUR_DOCKERHUB_USERNAME
  Password: YOUR_DOCKERHUB_PASSWORD
```

#### 📝 Jenkinsfile — CI Pipeline (App Build & Push):

Buat file `Jenkinsfile` di root repository aplikasi Anda:

```groovy
// ============================================================
// Jenkinsfile: CI Pipeline — Build & Push Docker Image
// Trigger: Setiap git push ke branch main
// ============================================================
pipeline {
    agent any

    environment {
        DOCKER_IMAGE   = 'YOUR_DOCKERHUB_USERNAME/cloud-infra-app'
        DOCKER_TAG     = "${BUILD_NUMBER}"     // Otomatis increment
        REGISTRY_CREDS = 'dockerhub-creds'     // ID credential di Jenkins
    }

    stages {
        // ── Stage 1: Checkout source code ──
        stage('Checkout') {
            steps {
                echo '📥 Checkout source code dari Git...'
                checkout scm
            }
        }

        // ── Stage 2: Lint Dockerfile ──
        stage('Lint Dockerfile') {
            steps {
                echo '🔍 Validasi Dockerfile...'
                sh '''
                    # Cek Dockerfile ada
                    test -f Dockerfile || (echo "❌ Dockerfile tidak ditemukan!" && exit 1)

                    # Basic lint: cek FROM instruction ada
                    grep -q "^FROM" Dockerfile || (echo "❌ Dockerfile harus punya FROM!" && exit 1)

                    echo "✅ Dockerfile valid"
                '''
            }
        }

        // ── Stage 3: Build Docker Image ──
        stage('Build Image') {
            steps {
                echo "🔨 Building Docker image: ${DOCKER_IMAGE}:${DOCKER_TAG}"
                sh """
                    docker build -t ${DOCKER_IMAGE}:${DOCKER_TAG} .
                    docker tag ${DOCKER_IMAGE}:${DOCKER_TAG} ${DOCKER_IMAGE}:latest
                """
            }
        }

        // ── Stage 4: Push ke Docker Hub ──
        stage('Push to Registry') {
            steps {
                echo '📦 Pushing image ke Docker Hub...'
                withCredentials([usernamePassword(
                    credentialsId: "${REGISTRY_CREDS}",
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh """
                        echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin
                        docker push ${DOCKER_IMAGE}:${DOCKER_TAG}
                        docker push ${DOCKER_IMAGE}:latest
                        docker logout
                    """
                }
            }
        }

        // ── Stage 5: Cleanup ──
        stage('Cleanup') {
            steps {
                echo '🧹 Cleanup local images...'
                sh """
                    docker rmi ${DOCKER_IMAGE}:${DOCKER_TAG} || true
                    docker rmi ${DOCKER_IMAGE}:latest || true
                """
            }
        }
    }

    post {
        success {
            echo """
            ✅ Pipeline SUKSES!
            Image: ${DOCKER_IMAGE}:${DOCKER_TAG}
            Docker Hub: https://hub.docker.com/r/${DOCKER_IMAGE}
            """
        }
        failure {
            echo '❌ Pipeline GAGAL! Cek logs di atas untuk detail error.'
        }
        always {
            // Bersihkan workspace
            cleanWs()
        }
    }
}
```

#### 🔄 Membuat Jenkins Job (Pipeline):

```
1. Jenkins Dashboard → New Item
2. Nama: "cloud-infra-app-ci"
3. Pilih: Pipeline → OK
4. Pipeline Section:
   - Definition: Pipeline script from SCM
   - SCM: Git
   - Repository URL: https://github.com/YOUR_USERNAME/cloud-infra-app.git
   - Branch: */main
   - Script Path: Jenkinsfile
5. Save → Build Now (test pertama)
```

**Struktur Repository Aplikasi:**
```
cloud-infra-app/
├── Jenkinsfile              # Pipeline definition
├── Dockerfile               # Docker build recipe (dari Day 5)
├── .dockerignore
├── nginx.conf
└── src/
    ├── index.html
    ├── styles.css
    └── app.js
```

#### 🔗 (Optional) Webhook — Auto Trigger saat Git Push:

```
1. GitHub Repository → Settings → Webhooks → Add webhook
2. Payload URL: http://YOUR_EC2_IP:8080/github-webhook/
3. Content type: application/json
4. Events: Just the push event
5. Save

Sekarang setiap git push → Jenkins otomatis trigger pipeline!
```

> ⚠️ **Catatan:** Webhook butuh EC2 bisa diakses dari internet (sudah terkonfigurasi di Security Group port 8080). Jika IP berubah, update webhook URL.

#### ✅ Verifikasi Pipeline:

```bash
# Setelah pipeline berjalan, verifikasi:

# 1. Cek di Jenkins Web UI — Build History → #1 → Console Output
# 2. Cek image di Docker Hub
docker pull YOUR_DOCKERHUB_USERNAME/cloud-infra-app:1
docker images | grep cloud-infra-app

# 3. Test run image yang baru di-build
docker run -d -p 8888:80 YOUR_DOCKERHUB_USERNAME/cloud-infra-app:1
curl http://localhost:8888
```

#### 📝 Deliverable Hari 7:
  - Jenkins berhasil running (Docker atau K3s) — accessible di `:8080` / `:30080`.
  - Plugin Docker Pipeline & Git terinstall.
  - Credential Docker Hub berhasil ditambahkan.
  - Jenkinsfile berhasil ditulis dengan 5 stages (Checkout → Lint → Build → Push → Cleanup).
  - Pipeline job dibuat & berhasil dijalankan minimal 1x.
  - Docker image ter-push ke Docker Hub dengan tag `BUILD_NUMBER`.
  - (Bonus) Webhook GitHub dikonfigurasi — auto trigger saat `git push`.

> 💡 **Koneksi ke Day 8:** Pipeline ini adalah *App CI Pipeline*. Di Day 8, kita akan membuat *Infra CI Pipeline* yang menjalankan Terraform + Ansible secara otomatis via Jenkins.

### DAY 8 — Infrastructure CI/CD & Automation
**Fokus:** Menerapkan CI/CD spesifik untuk menjalankan Terraform & Ansible secara otomatis melalui Jenkins — bukan dari laptop lokal.

#### 📖 Teori & Pemahaman:

**Kenapa Infrastruktur Harus via Pipeline, Bukan dari Laptop?**

| Aspek | Dari Laptop (Buruk ❌) | Dari Pipeline (Best Practice ✅) |
|---|---|---|
| **Konsistensi** | Beda laptop = beda versi Terraform | Semua pakai versi yang sama |
| **Audit** | Siapa yang jalankan `apply`? Tidak ada log | Git commit + Jenkins log = jejak lengkap |
| **Approval** | Engineer langsung apply tanpa review | Pipeline punya approval gate |
| **Credential** | AWS key di laptop engineer (risiko leak) | Key di Jenkins credential store (encrypted) |
| **Kolaborasi** | Conflict state, siapa yang terakhir apply? | Pipeline serialized, satu eksekusi per waktu |
| **Rollback** | Manual `terraform destroy` + re-apply | Git revert → pipeline otomatis rollback |

**Arsitektur Infra Pipeline:**

```
┌─────────────────────────────────────────────────────────────────┐
│                   INFRA CI/CD PIPELINE                           │
│                                                                 │
│  git push (infra repo)                                          │
│       │                                                         │
│       ▼                                                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  JENKINS INFRA PIPELINE                                 │   │
│  │                                                         │   │
│  │  Stage 1: Checkout Infra Code                           │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 2: Terraform Init + Validate                     │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 3: Terraform Plan (dry-run)                      │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 4: ⏸️  Manual Approval (Wajib review plan!)     │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 5: Terraform Apply                               │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 6: Ansible Playbook (Configure server)           │   │
│  │      │   → System update                                │   │
│  │      │   → SSH hardening                                │   │
│  │      │   → Install Docker + K3s                         │   │
│  │      │   → Install monitoring                           │   │
│  │      │                                                  │   │
│  │      ▼                                                  │   │
│  │  Stage 7: Smoke Test (verifikasi infra healthy)         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                          │                                      │
│               Hasil:     │                                      │
│               ✅ VPC + EC2 running                              │
│               ✅ K3s cluster ready                              │
│               ✅ Monitoring active                              │
└─────────────────────────────────────────────────────────────────┘
```

#### 📁 Struktur Repository Infrastruktur:

```
cloud-infra-repo/
├── Jenkinsfile.infra          # Pipeline khusus infrastruktur
├── terraform/                  # Semua kode Terraform (dari Day 3)
│   ├── main.tf
│   ├── variables.tf
│   ├── outputs.tf
│   ├── providers.tf
│   ├── security-groups.tf
│   └── terraform.tfvars       # ⚠️ Di-manage via Jenkins credentials
├── ansible/                    # Semua kode Ansible (dari Day 4)
│   ├── ansible.cfg
│   ├── inventory/
│   │   └── hosts.ini          # Auto-generate dari Terraform output
│   ├── playbooks/
│   │   ├── site.yml
│   │   ├── 01-system-update.yml
│   │   ├── 02-ssh-hardening.yml
│   │   ├── 03-install-docker.yml
│   │   ├── 04-install-k3s.yml
│   │   └── 05-install-monitoring.yml
│   └── files/
└── README.md
```

#### ⚙️ Setup Jenkins Credentials untuk Infra Pipeline:

**Credentials tambahan yang dibutuhkan:**

| ID Credential | Type | Isi | Keperluan |
|---|---|---|---|
| `aws-access-key` | Secret text | AWS Access Key ID | Terraform provider auth |
| `aws-secret-key` | Secret text | AWS Secret Access Key | Terraform provider auth |
| `ec2-ssh-key` | Secret file | File `.pem` SSH key | Ansible SSH ke EC2 |
| `my-public-ip` | Secret text | IP Anda + `/32` | Security Group rule |

```
Manage Jenkins → Credentials → System → Global credentials → Add Credentials

1. Kind: Secret text | ID: aws-access-key | Secret: AKIAXXXXXXXX
2. Kind: Secret text | ID: aws-secret-key | Secret: xxxxxxxxxxxx
3. Kind: Secret file | ID: ec2-ssh-key    | File: cloud-infra-key.pem
4. Kind: Secret text | ID: my-public-ip   | Secret: xxx.xxx.xxx.xxx/32
```

> ⚠️ **Best Practice:** Jangan hardcode AWS credentials di kode. Selalu simpan di Jenkins credential store yang ter-enkripsi.

#### 📝 Jenkinsfile.infra — Infrastructure Pipeline:

```groovy
// ============================================================
// Jenkinsfile.infra: Infrastructure CI/CD Pipeline
// Jalankan Terraform + Ansible secara otomatis & aman
// ============================================================
pipeline {
    agent any

    environment {
        TF_DIR     = 'terraform'
        ANSIBLE_DIR = 'ansible'
    }

    stages {
        // ── Stage 1: Checkout Infra Code ──
        stage('Checkout') {
            steps {
                echo '📥 Checkout infrastructure code...'
                checkout scm
            }
        }

        // ── Stage 2: Terraform Init & Validate ──
        stage('Terraform Init & Validate') {
            steps {
                echo '🔧 Initializing Terraform...'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY'),
                    string(credentialsId: 'my-public-ip', variable: 'MY_IP')
                ]) {
                    dir("${TF_DIR}") {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                            terraform init -input=false
                            terraform validate
                            echo "✅ Terraform initialized & validated"
                        '''
                    }
                }
            }
        }

        // ── Stage 3: Terraform Plan (Dry-Run) ──
        stage('Terraform Plan') {
            steps {
                echo '📋 Planning infrastructure changes...'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY'),
                    string(credentialsId: 'my-public-ip', variable: 'MY_IP')
                ]) {
                    dir("${TF_DIR}") {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                            terraform plan \
                              -var="my_ip=$MY_IP" \
                              -var="key_pair_name=cloud-infra-key" \
                              -out=tfplan \
                              -input=false

                            echo ""
                            echo "════════════════════════════════════════"
                            echo "  📋 TERRAFORM PLAN SELESAI"
                            echo "  Review output di atas sebelum approve!"
                            echo "════════════════════════════════════════"
                        '''
                    }
                }
            }
        }

        // ── Stage 4: Manual Approval (WAJIB!) ──
        stage('Approval') {
            steps {
                echo '⏸️ Menunggu approval manual...'
                input message: '''
                    🔍 Review Terraform Plan di atas.
                    Apakah perubahan infrastruktur sudah benar?

                    ⚠️ Setelah approve, Terraform AKAN membuat/mengubah resource di AWS!
                ''',
                ok: '✅ Approve & Apply'
            }
        }

        // ── Stage 5: Terraform Apply ──
        stage('Terraform Apply') {
            steps {
                echo '🚀 Applying infrastructure changes...'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    dir("${TF_DIR}") {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                            terraform apply -auto-approve tfplan

                            echo ""
                            echo "✅ Terraform Apply selesai!"
                            echo ""
                            terraform output
                        '''
                    }
                }
            }
        }

        // ── Stage 6: Generate Ansible Inventory ──
        stage('Generate Inventory') {
            steps {
                echo '📝 Generating Ansible inventory dari Terraform output...'
                withCredentials([
                    string(credentialsId: 'aws-access-key', variable: 'AWS_ACCESS_KEY_ID'),
                    string(credentialsId: 'aws-secret-key', variable: 'AWS_SECRET_ACCESS_KEY')
                ]) {
                    dir("${TF_DIR}") {
                        sh '''
                            export AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID
                            export AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY

                            # Ambil Public IP dari Terraform output
                            EC2_IP=$(terraform output -raw instance_public_ip)

                            # Generate inventory file
                            cat > ../ansible/inventory/hosts.ini << EOF
[k3s_server]
cloud-infra-server ansible_host=${EC2_IP}

[k3s_server:vars]
ansible_user=ubuntu

[all:vars]
ansible_python_interpreter=/usr/bin/python3
EOF

                            echo "✅ Inventory generated: EC2 IP = ${EC2_IP}"
                            cat ../ansible/inventory/hosts.ini
                        '''
                    }
                }
            }
        }

        // ── Stage 7: Ansible Playbook (Configure Server) ──
        stage('Ansible Configure') {
            steps {
                echo '⚙️ Running Ansible playbooks...'
                withCredentials([
                    file(credentialsId: 'ec2-ssh-key', variable: 'SSH_KEY_FILE')
                ]) {
                    dir("${ANSIBLE_DIR}") {
                        sh '''
                            # Set permission SSH key
                            cp $SSH_KEY_FILE /tmp/cloud-infra-key.pem
                            chmod 600 /tmp/cloud-infra-key.pem

                            # Tunggu EC2 SSH ready (max 2 menit)
                            echo "⏳ Menunggu EC2 SSH ready..."
                            for i in $(seq 1 24); do
                                EC2_IP=$(cat inventory/hosts.ini | grep ansible_host | head -1 | cut -d= -f2)
                                if ssh -o StrictHostKeyChecking=no -o ConnectTimeout=5 \
                                   -i /tmp/cloud-infra-key.pem ubuntu@$EC2_IP "echo ok" 2>/dev/null; then
                                    echo "✅ SSH ready!"
                                    break
                                fi
                                echo "  Attempt $i/24 — waiting 5s..."
                                sleep 5
                            done

                            # Jalankan master playbook
                            ANSIBLE_HOST_KEY_CHECKING=False \
                            ansible-playbook \
                              -i inventory/hosts.ini \
                              --private-key=/tmp/cloud-infra-key.pem \
                              playbooks/site.yml

                            # Cleanup SSH key
                            rm -f /tmp/cloud-infra-key.pem
                        '''
                    }
                }
            }
        }

        // ── Stage 8: Smoke Test ──
        stage('Smoke Test') {
            steps {
                echo '🧪 Running smoke tests...'
                withCredentials([
                    file(credentialsId: 'ec2-ssh-key', variable: 'SSH_KEY_FILE')
                ]) {
                    dir("${ANSIBLE_DIR}") {
                        sh '''
                            cp $SSH_KEY_FILE /tmp/cloud-infra-key.pem
                            chmod 600 /tmp/cloud-infra-key.pem

                            EC2_IP=$(cat inventory/hosts.ini | grep ansible_host | head -1 | cut -d= -f2)

                            echo "═══════════════════════════════════"
                            echo "  🧪 SMOKE TEST RESULTS"
                            echo "═══════════════════════════════════"

                            # Test 1: SSH access
                            echo "1. SSH Access..."
                            ssh -o StrictHostKeyChecking=no -i /tmp/cloud-infra-key.pem \
                                ubuntu@$EC2_IP "echo '✅ SSH OK'"

                            # Test 2: Docker running
                            echo "2. Docker..."
                            ssh -o StrictHostKeyChecking=no -i /tmp/cloud-infra-key.pem \
                                ubuntu@$EC2_IP "docker --version && echo '✅ Docker OK'"

                            # Test 3: K3s cluster healthy
                            echo "3. K3s Cluster..."
                            ssh -o StrictHostKeyChecking=no -i /tmp/cloud-infra-key.pem \
                                ubuntu@$EC2_IP "sudo kubectl get nodes && echo '✅ K3s OK'"

                            # Test 4: Node Exporter metrics
                            echo "4. Node Exporter..."
                            ssh -o StrictHostKeyChecking=no -i /tmp/cloud-infra-key.pem \
                                ubuntu@$EC2_IP "curl -s http://localhost:9100/metrics | head -1 && echo '✅ Monitoring OK'"

                            echo ""
                            echo "═══════════════════════════════════"
                            echo "  ✅ ALL SMOKE TESTS PASSED"
                            echo "  Server: $EC2_IP"
                            echo "═══════════════════════════════════"

                            rm -f /tmp/cloud-infra-key.pem
                        '''
                    }
                }
            }
        }
    }

    post {
        success {
            echo '''
            ═══════════════════════════════════════════
            ✅ INFRASTRUCTURE PIPELINE SUKSES!

            Hasil:
            • VPC + Public Subnet + IGW → Created
            • EC2 t2.micro → Running
            • Docker → Installed
            • K3s Cluster → Ready
            • Node Exporter → Active (:9100)
            • SSH Hardening → Applied
            ═══════════════════════════════════════════
            '''
        }
        failure {
            echo '❌ INFRASTRUCTURE PIPELINE GAGAL! Cek stage yang error di atas.'
        }
        always {
            cleanWs()
        }
    }
}
```

#### 🔄 Membuat Infra Pipeline Job di Jenkins:

```
1. Jenkins Dashboard → New Item
2. Nama: "cloud-infra-pipeline"
3. Pilih: Pipeline → OK
4. Pipeline Section:
   - Definition: Pipeline script from SCM
   - SCM: Git
   - Repository URL: https://github.com/YOUR_USERNAME/cloud-infra-repo.git
   - Branch: */main
   - Script Path: Jenkinsfile.infra
5. Save → Build Now
```

#### 🛡️ Best Practices Infra CI/CD:

| # | Best Practice | Alasan |
|---|---|---|
| 1 | **Selalu Plan sebelum Apply** | Preview perubahan, cegah "oops" moment |
| 2 | **Manual Approval wajib** | Tidak ada auto-apply tanpa human review |
| 3 | **Credentials di Jenkins, bukan di kode** | Cegah leak AWS key di Git |
| 4 | **Remote Backend (S3) untuk state** | Satu sumber kebenaran, state locking |
| 5 | **Smoke test setelah apply** | Verifikasi infra benar-benar healthy |
| 6 | **Git = single source of truth** | Semua perubahan infra via Git PR |
| 7 | **Jangan edit manual di console** | Terraform drift = masalah besar |
| 8 | **Pin versi provider & module** | Cegah breaking changes tak terduga |

#### 🔄 End-to-End Workflow (Skenario Sehari-hari):

```
Engineer ingin tambah Security Group rule baru:

1. 📝 Edit security-groups.tf di branch baru
2. 🔀 Buat Pull Request ke main
3. 👀 Tim review perubahan Terraform
4. ✅ PR di-merge ke main
5. 🔔 Jenkins auto-trigger Infra Pipeline
6. 📋 Terraform Plan → tampilkan perubahan
7. ⏸️ Engineer review plan → klik "Approve"
8. 🚀 Terraform Apply → SG rule ditambahkan
9. ⚙️ Ansible reconfigure (idempotent, skip jika tidak ada perubahan)
10. 🧪 Smoke test → semua OK
11. ✅ Done! Infra berubah secara aman & terdokumentasi
```

#### 📝 Deliverable Hari 8:
  - Repository infrastruktur terstruktur (Terraform + Ansible dalam 1 repo).
  - Jenkins credentials (AWS key, SSH key, IP) berhasil ditambahkan.
  - Jenkinsfile.infra berhasil ditulis dengan 8 stages.
  - Pipeline berhasil dijalankan: Terraform → Approval → Apply → Ansible → Smoke Test.
  - Inventory Ansible auto-generate dari Terraform output.
  - Smoke test lolos semua (SSH, Docker, K3s, Monitoring).
  - (Bonus) Simulasi perubahan infra: edit SG → git push → pipeline → infra berubah otomatis.

> 💡 **Koneksi ke Day 9:** Sekarang kita punya 2 pipeline — *App Pipeline* (Day 7) untuk build image dan *Infra Pipeline* (Day 8) untuk provisioning. Di Day 9, Argo CD akan menjadi jembatan terakhir: auto-deploy aplikasi ke K3s setiap kali manifest berubah di Git.

### DAY 9 — GitOps for Cluster Management with Argo CD
**Fokus:** Menerapkan metode *Pull-based deployment* di Kubernetes — Argo CD otomatis sync manifest dari Git ke cluster.

#### 📖 Teori & Pemahaman:

**Apa itu GitOps?**
GitOps = **Git sebagai single source of truth untuk state cluster Kubernetes.** Semua perubahan deployment dilakukan via Git commit, bukan `kubectl apply` manual.

**Push-based CD (Jenkins) vs Pull-based CD (Argo CD):**

| Aspek | Push (Jenkins - Day 7) | Pull (Argo CD - Day 9) |
|---|---|---|
| **Cara kerja** | Jenkins *push* perubahan ke cluster | Argo CD *pull/watch* perubahan dari Git |
| **Trigger** | External event (webhook, cron) | Argo CD polling Git setiap 3 menit |
| **Credential** | Jenkins butuh kubeconfig cluster | Argo CD sudah di dalam cluster |
| **Drift detection** | Tidak tahu jika ada perubahan manual | Deteksi otomatis & reconcile |
| **Security** | CI server punya akses ke cluster (risiko) | Cluster pull sendiri (lebih aman) |
| **Best for** | Build & push image (CI) | Deploy manifest ke cluster (CD) |

> 💡 **Best Practice Enterprise:** Jenkins untuk **CI** (build image), Argo CD untuk **CD** (deploy ke K8s). Keduanya saling melengkapi.

**Arsitektur GitOps dalam Kurikulum Kita:**

```
┌─────────────────────────────────────────────────────────────────┐
│                     GITOPS WORKFLOW                              │
│                                                                 │
│  ┌──────────────┐    Jenkins CI (Day 7)    ┌────────────────┐  │
│  │ App Source    │ ──── build & push ─────► │  Docker Hub    │  │
│  │ Repo (code)  │                          │  (Registry)    │  │
│  └──────────────┘                          └────────────────┘  │
│         │                                                       │
│         │ Jenkins updates image tag                              │
│         ▼                                                       │
│  ┌──────────────┐                          ┌────────────────┐  │
│  │ K8s Manifest │ ◄── Argo CD watches ──── │  Argo CD       │  │
│  │ Repo (YAML)  │     (every 3 min)        │  (in K3s)      │  │
│  └──────┬───────┘                          └───────┬────────┘  │
│         │                                          │            │
│         │  Git = desired state                     │ reconcile  │
│         │                                          ▼            │
│         │                                  ┌────────────────┐  │
│         └─── state harus sama ───────────► │  K3s Cluster   │  │
│                                            │  (actual state)│  │
│                                            └────────────────┘  │
│                                                                 │
│  Jika actual ≠ desired → Argo CD otomatis sync!                │
└─────────────────────────────────────────────────────────────────┘
```

#### 📁 Struktur K8s Manifest Repository:

```
cloud-infra-k8s-manifests/          # Repo TERPISAH dari app source code
├── apps/
│   └── nginx-app/
│       ├── namespace.yml            # Namespace cloud-infra
│       ├── deployment.yml           # Deployment (image tag di sini!)
│       └── service.yml              # Service NodePort
├── monitoring/
│   ├── namespace.yml
│   ├── prometheus-config.yml
│   ├── prometheus-deployment.yml
│   └── grafana-deployment.yml
├── argocd/
│   └── application.yml              # Argo CD Application CR
└── README.md
```

> ⚠️ **Kenapa manifest repo TERPISAH dari app repo?** Agar perubahan kode aplikasi (trigger CI build) tidak bercampur dengan perubahan deployment config (trigger CD sync). Ini standard GitOps.

#### 🔧 Instalasi Argo CD di K3s:

```bash
# SSH ke EC2
ssh -i ~/.ssh/cloud-infra-key.pem ubuntu@YOUR_EC2_IP

# ── 1. Buat namespace untuk Argo CD ──
kubectl create namespace argocd

# ── 2. Install Argo CD via official manifest ──
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

# ── 3. Tunggu semua pods ready (1-3 menit) ──
kubectl get pods -n argocd -w
# Tunggu sampai semua STATUS = Running

# ── 4. Expose Argo CD via NodePort ──
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort", "ports": [{"port": 443, "targetPort": 8080, "nodePort": 30443}]}}'

# ── 5. Ambil initial admin password ──
kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d
echo ""

# ── 6. Akses Argo CD Web UI ──
# Buka browser: https://YOUR_EC2_IP:30443
# Username: admin
# Password: (dari step 5)
```

> 💡 **Tip:** Browser akan warning "Not Secure" karena self-signed SSL certificate. Klik "Advanced → Proceed" untuk melanjutkan.

#### 📦 Install Argo CD CLI (Optional — di lokal):

```bash
# Linux/WSL
curl -sSL -o argocd https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64
chmod +x argocd
sudo mv argocd /usr/local/bin/

# Login via CLI
argocd login YOUR_EC2_IP:30443 --username admin --password YOUR_PASSWORD --insecure

# Lihat cluster yang terdaftar
argocd cluster list
```

#### 📝 Konfigurasi Argo CD Application:

**Metode 1: Via Web UI**
```
1. Argo CD Dashboard → + NEW APP
2. Application Name: nginx-app
3. Project: default
4. Sync Policy: Automatic (centang Auto-Sync & Self Heal)
5. Repository URL: https://github.com/YOUR_USERNAME/cloud-infra-k8s-manifests.git
6. Path: apps/nginx-app
7. Cluster URL: https://kubernetes.default.svc  (cluster lokal)
8. Namespace: cloud-infra
9. Klik CREATE
```

**Metode 2: Via YAML Manifest (Recommended — GitOps way):**

**`argocd/application.yml` — Argo CD Application CR:**
```yaml
# ============================================================
# Argo CD Application: Nginx App
# Argo CD akan watch Git repo ini dan auto-sync ke cluster
# ============================================================
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: nginx-app
  namespace: argocd
spec:
  project: default

  # ── Source: Git repository yang berisi manifest K8s ──
  source:
    repoURL: https://github.com/YOUR_USERNAME/cloud-infra-k8s-manifests.git
    targetRevision: main       # Branch yang di-watch
    path: apps/nginx-app       # Folder yang berisi manifest

  # ── Destination: Cluster & namespace target deploy ──
  destination:
    server: https://kubernetes.default.svc   # Cluster lokal (K3s)
    namespace: cloud-infra

  # ── Sync Policy: Otomatis sync & self-heal ──
  syncPolicy:
    automated:
      prune: true              # Hapus resource yang tidak ada di Git
      selfHeal: true           # Jika ada perubahan manual, revert ke Git
    syncOptions:
      - CreateNamespace=true   # Buat namespace jika belum ada
```

**`argocd/application-monitoring.yml` — Monitoring Stack:**
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: monitoring-stack
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://github.com/YOUR_USERNAME/cloud-infra-k8s-manifests.git
    targetRevision: main
    path: monitoring
  destination:
    server: https://kubernetes.default.svc
    namespace: monitoring
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

```bash
# Apply Argo CD Applications
kubectl apply -f argocd/application.yml
kubectl apply -f argocd/application-monitoring.yml

# Verifikasi di Argo CD
kubectl get applications -n argocd
# NAME               SYNC STATUS   HEALTH STATUS
# nginx-app          Synced        Healthy
# monitoring-stack   Synced        Healthy
```

#### 🔄 Simulasi Auto-Sync — Demo GitOps in Action:

**Skenario: Update image tag di Git → Argo CD otomatis deploy versi baru.**

```bash
# ── STEP 1: Edit manifest di Git repo (dari laptop) ──
cd cloud-infra-k8s-manifests/

# Ubah image tag di deployment.yml
# SEBELUM:
#   image: nginx:alpine
# SESUDAH:
#   image: YOUR_DOCKERHUB_USERNAME/cloud-infra-app:2
```

Edit file `apps/nginx-app/deployment.yml`:
```yaml
      containers:
        - name: nginx
          image: YOUR_DOCKERHUB_USERNAME/cloud-infra-app:2  # ← Ganti tag!
```

```bash
# ── STEP 2: Commit & Push ──
git add .
git commit -m "chore: update nginx-app image to v2"
git push origin main

# ── STEP 3: Tunggu Argo CD sync (max 3 menit) ──
# Atau trigger manual:
argocd app sync nginx-app

# ── STEP 4: Verifikasi di cluster ──
kubectl get pods -n cloud-infra -w
# Pod lama akan Terminating, pod baru dengan image v2 akan Running

kubectl describe deployment nginx-app -n cloud-infra | grep Image
# Image: YOUR_DOCKERHUB_USERNAME/cloud-infra-app:2  ✅
```

**Lihat di Argo CD Web UI:**
```
https://YOUR_EC2_IP:30443 → nginx-app
Status: Synced ✅ | Healthy ✅
Last Sync: 30 seconds ago
```

#### 🛡️ Simulasi Self-Heal — Argo CD Revert Manual Changes:

```bash
# ── Seseorang mengubah deployment secara manual (bukan via Git) ──
kubectl scale deployment nginx-app -n cloud-infra --replicas=5

# ── Cek: sekarang 5 replika ──
kubectl get deployment -n cloud-infra
# nginx-app   5/5   5   5

# ── Tunggu ~30 detik... Argo CD mendeteksi drift! ──
# Argo CD akan revert ke 2 replika (sesuai Git manifest)

kubectl get deployment -n cloud-infra
# nginx-app   2/2   2   2  ← Kembali ke 2 sesuai Git!
```

> 💡 **Self-Heal** memastikan cluster SELALU sesuai dengan apa yang ada di Git. Perubahan manual di cluster akan otomatis di-revert oleh Argo CD. Ini mencegah *configuration drift*.

#### 🔗 Integrasi Jenkins + Argo CD (Full CI/CD Flow):

```
Jenkins (CI - Day 7)                  Argo CD (CD - Day 9)
┌──────────────────────┐              ┌──────────────────────┐
│ 1. Checkout code     │              │                      │
│ 2. Build Docker image│              │ 5. Detect manifest   │
│ 3. Push to Docker Hub│              │    change in Git     │
│ 4. Update image tag  │──git push──►│ 6. Pull new manifest │
│    di manifest repo  │              │ 7. Apply to K3s      │
└──────────────────────┘              │ 8. Verify healthy    │
                                      └──────────────────────┘
```

**Update Jenkinsfile (Day 7) — tambah stage update manifest:**
```groovy
        // ── Stage tambahan: Update K8s Manifest Tag ──
        stage('Update Manifest') {
            steps {
                echo '📝 Updating K8s manifest with new image tag...'
                withCredentials([
                    string(credentialsId: 'github-token', variable: 'GH_TOKEN')
                ]) {
                    sh """
                        # Clone manifest repo
                        git clone https://\$GH_TOKEN@github.com/YOUR_USERNAME/cloud-infra-k8s-manifests.git
                        cd cloud-infra-k8s-manifests

                        # Update image tag di deployment.yml
                        sed -i 's|image: .*cloud-infra-app:.*|image: ${DOCKER_IMAGE}:${DOCKER_TAG}|' \\
                            apps/nginx-app/deployment.yml

                        # Commit & push
                        git config user.name "Jenkins CI"
                        git config user.email "jenkins@cloud-infra"
                        git add .
                        git commit -m "ci: update image tag to ${DOCKER_TAG}"
                        git push origin main

                        echo "✅ Manifest updated → Argo CD will auto-sync!"
                    """
                }
            }
        }
```

#### ✅ Verifikasi Argo CD:

```bash
# ── Dari EC2 ──

# Lihat semua Argo CD applications
kubectl get applications -n argocd

# Detail sync status
argocd app get nginx-app

# History sync
argocd app history nginx-app

# Lihat semua resource yang di-manage
argocd app resources nginx-app

# Force sync manual (jika perlu)
argocd app sync nginx-app

# Rollback ke versi sebelumnya
argocd app rollback nginx-app 1    # Rollback ke revision 1
```

#### 📝 Deliverable Hari 9:
  - Argo CD berhasil ter-install di K3s namespace `argocd`.
  - Argo CD Web UI accessible di `https://EC2_IP:30443`.
  - Application CR dibuat — Argo CD connected ke Git manifest repo.
  - Status: `Synced` & `Healthy` di Argo CD dashboard.
  - **Auto-sync demo:** Edit manifest di Git → push → Argo CD otomatis deploy.
  - **Self-heal demo:** Manual `kubectl scale` → Argo CD revert ke state Git.
  - (Bonus) Jenkins pipeline update image tag → commit ke manifest repo → Argo CD auto-deploy.

> 💡 **Day 10 Preview:** Besok semua komponen ini digabung menjadi satu platform end-to-end: `git push` → Jenkins build → push image → update manifest → Argo CD deploy → Prometheus monitor → self-heal jika pod down.

### DAY 10 — Capstone Project: Auto-Healing Cloud Infrastructure Platform
**Fokus:** Membangun platform infrastruktur yang mampu *self-provision*, *self-configure*, dan *self-heal* secara otomatis — end-to-end dari IaC hingga GitOps (100% Free Tier).
- **Skenario:** *Ketika seorang engineer melakukan `git push`, seluruh rantai otomatisasi berjalan sendiri: infrastruktur cloud terprovision, cluster K3s terkonfigurasi, aplikasi ter-deploy, dan sistem monitoring aktif memantau kesehatan cluster. Jika ada pod yang down, alert langsung dikirim dan sistem bereaksi.*
- **Komponen Utama:**
  - **Terraform** — Provisioning VPC, Public Subnet, Security Group, dan EC2 `t2.micro` (Free Tier) sebagai node K3s.
  - **Ansible** — Hardening OS, install K3s, dan deploy Prometheus + Alertmanager ke node.
  - **Jenkins** — Orkestrasi pipeline Infra (Terraform + Ansible) dan pipeline App (Build image → push → update manifest).
  - **Argo CD** — GitOps controller yang auto-sync manifest K8s dari Git ke cluster K3s.
  - **Prometheus + Alertmanager** — Monitoring cluster health dan trigger alert jika pod/node down.
  - **Docker Hub** — Container registry gratis untuk menyimpan Docker image hasil build.
- **Siklus Pipeline (End-to-End):**
  1. **Jenkins (Infra Pipeline)**: Mengeksekusi Terraform untuk membangun VPC & EC2 Free Tier, dilanjutkan memanggil Ansible untuk menginstal K3s dan agen monitoring (Prometheus Node Exporter + Alertmanager) di VM tersebut.
  2. **Jenkins (App Pipeline)**: Melakukan *build* Docker image → *push* ke Docker Hub → *commit* update versi tag manifest di Git repository.
  3. **Argo CD (GitOps)**: Mendeteksi perubahan manifest di Git, dan otomatis men-deploy komponen terbaru ke cluster K3s secara sinkron.
  4. **Self-Healing Simulation**: Menghapus pod secara manual (`kubectl delete pod`) → Prometheus mendeteksi pod down → Alertmanager mengirim alert → Kubernetes *self-heal* dengan me-reschedule pod otomatis → Argo CD memastikan state cluster kembali sesuai manifest Git.
- **Deliverable Presentasi:**
  - Demo live: `git push` satu kali → infrastruktur berubah otomatis.
  - Grafana/Prometheus dashboard menampilkan cluster health secara real-time.
  - Simulasi *self-healing*: pod dihapus → recovered otomatis dalam hitungan detik.

---

## 🏆 Capstone Project Architecture {#capstone-project}

**"Auto-Healing Cloud Infrastructure Platform"** — Sistem infrastruktur cloud yang mampu *self-provision*, *self-configure*, dan *self-heal* secara otomatis dari satu `git push`.

```text
┌─────────────────────────────────────────────────────────────────────┐
│                        TRIGGER: git push                            │
└──────────────────────────────┬──────────────────────────────────────┘
                               │
                               ▼
┌──────────────────────────────────────────────────────────────────────┐
│                      JENKINS (Orchestrator)                          │
│                                                                      │
│  ┌─────────────────────────┐    ┌────────────────────────────────┐  │
│  │   (1) INFRA PIPELINE    │    │      (2) APP PIPELINE          │  │
│  │  Checkout               │    │  Checkout                      │  │
│  │  → Terraform Plan/Apply │    │  → Lint Dockerfile             │  │
│  │  → Ansible Playbook     │    │  → Build Docker Image          │  │
│  │    (K3s + Prometheus +  │    │  → Push to Docker Hub          │  │
│  │     Alertmanager)       │    │  → Update K8s Manifest Tag     │  │
│  └────────────┬────────────┘    └──────────────┬─────────────────┘  │
└───────────────┼──────────────────────────────── ┼───────────────────┘
                │                                  │
                ▼                                  ▼
┌──────────────────────────┐         ┌─────────────────────────────┐
│  AWS Free Tier           │         │  GitHub                     │
│  ├── VPC + Public Subnet │         │  ├── App Source Repo        │
│  ├── Security Group      │         │  └── K8s Manifest Repo ─────┼──┐
│  └── EC2 t2.micro        │         └─────────────────────────────┘  │
│       └── K3s Cluster    │                                           │
│            ├── App Pods  │◄─────────────────────────────────────────┘
│            └── Monitoring│         (4) Auto-Sync & Deploy
│                 Stack    │◄──── Argo CD (GitOps Controller)
└──────────────┬───────────┘              │
               │                          │ Watches Git Manifest Repo
               │ Metrics & Alerts         │ Reconciles Cluster State
               ▼                          │
┌──────────────────────────┐             (3) Update Manifest Tag
│  MONITORING & SELF-HEAL  │
│  Prometheus → scrape     │
│  Alertmanager → alert    │   ══► SELF-HEALING LOOP:
│  K8s Controller → rescue │        Pod down → Alert fired
│  Argo CD → reconcile     │        K8s reschedules pod
└──────────────────────────┘        Argo CD confirms state = Git
```

**Tech Stack Summary (100% Free Tier):**

| Layer | Tool | Biaya |
|---|---|---|
| Cloud VM | AWS EC2 `t2.micro` | Free Tier (750 jam/bulan) |
| IaC | Terraform + S3 Remote Backend | Gratis |
| Config Mgmt | Ansible | Gratis (open source) |
| Kubernetes | K3s (self-managed) | Gratis |
| CI/CD | Jenkins (Docker) | Gratis (self-hosted) |
| GitOps | Argo CD | Gratis (open source) |
| Container Registry | Docker Hub | Gratis (public repo) |
| Monitoring | Prometheus + Alertmanager | Gratis (open source) |

---


## 📚 Learning Resources {#resources}

- **Cloud Providers:** [AWS Skill Builder](https://skillbuilder.aws/) | [Tencent Cloud Docs](https://www.tencentcloud.com/document)
- **Terraform:** [Terraform Learn Tutorials](https://developer.hashicorp.com/terraform/tutorials)
- **Ansible:** [Ansible Documentation](https://docs.ansible.com/)
- **Jenkins:** [Jenkins Pipeline Tutorial](https://www.jenkins.io/doc/book/pipeline/)
- **Kubernetes:** [Kubernetes Basics](https://kubernetes.io/docs/tutorials/kubernetes-basics/)
- **Argo CD:** [Argo CD Getting Started](https://argo-cd.readthedocs.io/en/stable/getting_started/)
