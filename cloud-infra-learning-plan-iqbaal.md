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
- **Teori:** VPC (Virtual Private Cloud), Subnet (Public vs Private), Route Tables, Internet Gateway. *Catatan Free Tier: Managed NAT Gateway berbayar mahal, kita akan belajar konsepnya namun praktiknya menggunakan pendekatan Free Tier (Public Subnet).*
- **Praktik:**
  - Membuat VPC dengan arsitektur Public Subnet (agar CVM/EC2 Free tier tetap gratis tanpa butuh NAT Gateway berbayar).
  - Mengonfigurasi *Security Group* secara ketat agar hanya IP tertentu (IP lokal Anda) yang bisa melakukan SSH (port 22) ke server.
  - Verifikasi keamanan *inbound* dan *outbound* rules.

### DAY 3 — Infrastructure as Code (IaC) with Terraform
**Fokus:** Mengubah penyediaan infrastruktur manual di console menjadi barisan kode.
- **Teori:** Konsep Declarative IaC, *Providers*, *State file* (`terraform.tfstate`), Variables & Outputs. Keuntungan menggunakan IaC di enterprise.
- **Praktik:**
  - Menulis *code* Terraform untuk men-*deploy* ulang VPC dan EC2/CVM yang dibuat di Hari ke-2.
  - Menjalankan `terraform init`, `plan`, `apply`, dan `destroy`.
  - Setup *Remote Backend* (menyimpan state file secara terpusat di AWS S3/Tencent COS dengan fitur *state locking*).

### DAY 4 — Configuration Management with Ansible
**Fokus:** Melakukan *hardening* OS dan konfigurasi puluhan server secara otomatis.
- **Teori:** *Push mechanism*, Architecture (Control Node & Managed Nodes), Inventory, Playbooks, konsep *Idempotency*.
- **Praktik:**
  - Membuat Ansible `inventory` dinamis dari server cloud yang di-deploy via Terraform.
  - Menulis Ansible Playbook (YAML) untuk *system update*, *hardening* SSH (disable password & root login), dan instalasi agen monitoring.
  - Mengeksekusi *playbook* ke *remote cloud server*.

### DAY 5 — Containerization with Docker
**Fokus:** Mengemas *software* agar berjalan konsisten, persiapan menuju Kubernetes.
- **Teori:** Arsitektur Docker, Perbedaan Virtual Machine vs Container, Dockerfile, Container Networking.
- **Praktik:**
  - Menulis `Dockerfile`.
  - Melakukan *build*, *run*, dan *troubleshoot* Docker container.
  - Setup Container Registry (AWS ECR / Docker Hub) dan *push image* ke cloud.

### DAY 6 — Kubernetes (K8s) Cluster Administration
**Fokus:** Menjadi administrator cluster Kubernetes (Bukan sekadar *deploy* aplikasi).
- **Teori:** K8s Architecture (Control Plane, Worker Node, Kubelet), Pods, Deployments, Services. *Catatan Free Tier: Managed K8s (EKS/TKE) membebankan biaya per jam. Kita akan menggunakan self-managed K3s (Lightweight K8s) yang sangat ringan dan 100% gratis.*
- **Praktik:**
  - Menjalankan K8s lokal dengan `minikube` **ATAU** instalasi cluster K3s secara manual di atas VM (EC2/CVM) Free Tier.
  - Menganalisa *node status* dan *cluster health*.
  - Melakukan *deploy* aplikasi (Nginx) menggunakan `kubectl` dan mengaksesnya lewat `NodePort` (karena LoadBalancer berbayar).

### DAY 7 — Continuous Integration (CI) with Jenkins
**Fokus:** Membangun server otomatisasi (CI) untuk mem-build *artifact* (Docker Images/Code).
- **Teori:** Konsep CI, Jenkins Architecture (Master-Agent), Jenkinsfile (Declarative Pipeline).
- **Praktik:**
  - Instalasi Jenkins di atas VM menggunakan Docker.
  - Menulis *Declarative Pipeline* untuk: `Checkout Code` -> `Lint Dockerfile` -> `Build Docker Image` -> `Push to Registry`.

### DAY 8 — Infrastructure CI/CD & Automation
**Fokus:** Menerapkan CI/CD spesifik untuk menjalankan *Infrastructure as Code* (Terraform) & Ansible.
- **Teori:** Bahaya mengeksekusi Terraform dari laptop lokal engineer. Pentingnya membangun *Infrastructure Pipeline*.
- **Praktik:**
  - Membuat pipeline Jenkins khusus untuk mengeksekusi Terraform dan Ansible.
  - *Pipeline Stage*: `Checkout` -> `Terraform Plan/Apply` -> `Ansible Configure (Otomatis instalasi K3s ke VM Free Tier)`.
  - Otomatisasi perubahan infrastruktur secara kolaboratif melalui Git *push* (Infrastruktur terpusat).

### DAY 9 — GitOps for Cluster Management with Argo CD
**Fokus:** Menerapkan metode *Pull-based deployment* di Kubernetes menggunakan standar GitOps.
- **Teori:** Apa itu GitOps? *Infrastructure state* vs *Cluster state*. Arsitektur Argo CD.
- **Praktik:**
  - Menginstal Argo CD di dalam cluster Kubernetes.
  - Mengonfigurasi Argo CD untuk memantau Git Repository yang berisi *manifest* K8s.
  - Simulasi sinkronisasi otomatis (*auto-sync*): Mengubah file *manifest* K8s di Git, dan melihat Argo CD otomatis merekonsiliasi cluster sesuai kode di Git.

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
