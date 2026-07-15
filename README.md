<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/5/50/Oracle_logo.svg" alt="Oracle Logo" width="240" />

<h1 align="center">Kitab Oracle Cloud 🗄️ 🇮🇩<br><sub>(Always Free Tier)</sub></h1>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=20&pause=1000&color=F80000&center=true&vCenter=true&width=680&lines=ARM+Compute+%2B+RAM+Always+Free;Kuota+Mengikuti+Kebijakan+Oracle;Linux+VM+Untuk+Docker;Bangun+Server+Modal+Rp+0" alt="Typing SVG" />
</p>

Kumpulan panduan, *script* automasi, dan proyek *open-source* untuk memanfaatkan **Oracle Cloud Always Free Tier** — resource compute tanpa biaya selama akun, kapasitas region, dan penggunaan memenuhi ketentuan program. Dokumentasi Oracle yang diaudit pada **2026-07-16** menyebut ekuivalen **2 OCPU + 12 GB RAM** untuk Ampere A1 pada tenancy Always Free; cek limit tenancy Anda sebelum provisioning.
Dibangun untuk developer & *indie hacker* Indonesia yang butuh server beneran (Docker, database, self-hosting) dengan biaya Rp 0.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Stars](https://img.shields.io/github/stars/ridloabelian/awesome-oracle-free-id?style=flat&color=F80000)](https://github.com/ridloabelian/awesome-oracle-free-id/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/ridloabelian/awesome-oracle-free-id?style=flat&color=F80000)](https://github.com/ridloabelian/awesome-oracle-free-id/commits/main)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](LICENSE)

</div>

> **Audit:** Terakhir diverifikasi **2026-07-16**. Kuota dan kebijakan dapat berubah; cek [referensi resource resmi](https://docs.oracle.com/en-us/iaas/Content/FreeTier/resourceref.htm) dan limit tenancy sebelum implementasi.
>
> **Disclaimer:** Proyek komunitas independen. Tidak berafiliasi dengan atau didukung oleh Oracle Corporation. Oracle dan logonya merupakan merek dagang pemiliknya.

> 🗺️ **Bagian dari seri [Stack Nol Rupiah](https://github.com/ridloabelian/awesome-rp0-id)** — peta lengkap bootstrap gratisan Rp 0 untuk indie hacker Indonesia.

> 🔗 **Seri saudara:** [**Kitab Cloudflare**](https://github.com/ridloabelian/awesome-cloudflare-id) (edge/web) · [**Kitab Google**](https://github.com/ridloabelian/awesome-google-free-id) (automasi bisnis) · [**Kitab Supabase**](https://github.com/ridloabelian/awesome-supabase-id) (database/auth) · [**Kitab Telegram**](https://github.com/ridloabelian/awesome-telegram-infra-id) (komunikasi/notifikasi). **Oracle melengkapi seri dengan Linux VM untuk workload yang membutuhkan kontrol host, Docker, atau self-hosting.**

Berbeda dari layanan *serverless* dalam seri ini, Oracle Cloud menyediakan **Linux VM** yang dapat diakses lewat SSH untuk menjalankan Docker, database, dan aplikasi self-hosted. Resource tetap tanpa biaya hanya selama berada dalam limit Always Free serta mematuhi kebijakan akun dan penggunaan Oracle.

**Kriteria Kurasi:**
- Memanfaatkan resource berlabel Oracle Cloud Always Free, bukan kredit trial sementara.
- Automasi *provisioning*, self-hosting, atau IaC (Terraform/script).
- *Open-source* dan idealnya masih aktif di-*maintain*.
- Bermanfaat untuk developer & solopreneur Indonesia.


**Status kurasi:** `Official` = dikelola vendor/organisasi resmi · `Community` = proyek komunitas · `Experimental` = contoh/POC, audit sebelum produksi · `Archived` = read-only/tidak aktif. Lihat [audit katalog lengkap](CATALOG_AUDIT.md) (status, stars, last push, dan sumber README upstream; diverifikasi 2026-07-16).

---

## 💰 Apa Saja yang Termasuk Always Free?

| Sumber Daya | Batas Always Free | Catatan |
|-------------|-------------------|---------|
| **ARM Ampere A1** | Ekuivalen 2 OCPU + 12 GB RAM untuk tenancy Always Free | Dapat dibagi sesuai limit, boot volume, region, dan kapasitas akun. |
| **VM AMD (x86)** | 2× VM (1 vCPU + 1 GB RAM masing-masing) | Untuk beban ringan / kompatibilitas x86. |
| **Block Storage** | 200 GB total | Untuk disk VM. |
| **Object Storage** | 20 GB (10 GB standard + 10 GB archive) | Mirip S3. |
| **Bandwidth keluar** | 10 TB/bulan | Sangat besar, cukup untuk banyak layanan. |
| **Load Balancer** | 1 (10 Mbps) | Gratis. |
| **Database Otonom** | 2× (20 GB masing-masing) | Oracle Autonomous DB. |

> ⚠️ **Penting & jujur:** (1) Oracle menyatakan kebanyakan pengguna memerlukan nomor ponsel dan kartu kredit untuk verifikasi; penggunaan di atas limit dapat berbiaya setelah akun di-upgrade. (2) Kapasitas ARM dapat mengalami **"Out of Capacity"** di region ramai. (3) Resource idle dapat di-*reclaim* sesuai kebijakan; jalankan workload nyata dan siapkan backup. (4) Pilih home region dengan hati-hati dan cek limit langsung di Console.

---

## Daftar Isi
- [💰 Apa Saja yang Termasuk Always Free?](#-apa-saja-yang-termasuk-always-free)
- [🎯 Auto-Provisioning ARM (Anti "Out of Capacity")](#-auto-provisioning-arm-anti-out-of-capacity)
- [☸️ Kubernetes (k3s/k8s) pada Always Free](#️-kubernetes-k3sk8s-pada-always-free)
- [🚀 PaaS Self-Hosted (Vercel/Heroku Alternative)](#-paas-self-hosted-vercelheroku-alternative)
- [🛡️ Networking & Privasi (VPN/Pi-hole)](#️-networking--privasi-vpnpi-hole)
- [📦 Backend & App Self-Hosted](#-backend--app-self-hosted)
- [🏗️ Terraform & IaC](#️-terraform--iac)
- [📚 Referensi & Panduan](#-referensi--panduan)
- [📄 Tips Cepat](#-tips-cepat)

---

## 🎯 Auto-Provisioning ARM (Anti "Out of Capacity")
Masalah #1 Oracle Free: kapasitas ARM sering habis. *Script* ini otomatis mencoba terus sampai berhasil.

| Nama | Deskripsi |
|------|-----------|
| [mohankumarpaluru/oracle-freetier-instance-creation](https://github.com/mohankumarpaluru/oracle-freetier-instance-creation) ![](https://img.shields.io/github/stars/mohankumarpaluru/oracle-freetier-instance-creation?style=flat&label=%E2%98%85&color=F80000) | Script Python yang terus mencoba membuat instance ARM gratis sampai berhasil. Paling populer & andal untuk melawan "Out of Capacity". |
| [HotNoob/Oracle-Free-Arm-VPS-PS](https://github.com/HotNoob/Oracle-Free-Arm-VPS-PS) ![](https://img.shields.io/github/stars/HotNoob/Oracle-Free-Arm-VPS-PS?style=flat&label=%E2%98%85&color=F80000) | Script PowerShell sederhana yang otomatis mencoba membuat VPS ARM di Oracle. Cocok untuk pengguna Windows. |
| [futchas/oracle-cloud-free-arm-instance](https://github.com/futchas/oracle-cloud-free-arm-instance) ![](https://img.shields.io/github/stars/futchas/oracle-cloud-free-arm-instance?style=flat&label=%E2%98%85&color=F80000) | Script Bash untuk membuat instance ARM menggunakan OCI CLI resmi. |

## ☸️ Kubernetes (k3s/k8s) pada Always Free
Jalankan k3s/k8s sesuai limit compute tenancy — utamakan belajar, eksperimen, atau workload kecil dengan backup.

| Nama | Deskripsi |
|------|-----------|
| [garutilorenzo/k3s-oci-cluster](https://github.com/garutilorenzo/k3s-oci-cluster) ![](https://img.shields.io/github/stars/garutilorenzo/k3s-oci-cluster?style=flat&label=%E2%98%85&color=F80000) | Deploy cluster Kubernetes (k3s) gratis penuh menggunakan Terraform di Oracle Always Free. Lengkap & terawat. |
| [nce/oci-free-cloud-k8s](https://github.com/nce/oci-free-cloud-k8s) ![](https://img.shields.io/github/stars/nce/oci-free-cloud-k8s?style=flat&label=%E2%98%85&color=F80000) | Panduan & IaC untuk menjalankan Kubernetes tersedia melalui Always Free di Oracle Cloud. |
| [r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure](https://github.com/r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure) ![](https://img.shields.io/github/stars/r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure?style=flat&label=%E2%98%85&color=F80000) | Deploy cluster k3s otomatis penuh, termasuk Infrastructure as Code. |

## 🚀 PaaS Self-Hosted (Vercel/Heroku Alternative)
Punya "Vercel/Heroku" sendiri di VPS gratis — deploy app dengan git push, tersedia melalui Always Free.

| Nama | Deskripsi |
|------|-----------|
| [coollabsio/coolify](https://github.com/coollabsio/coolify) ![](https://img.shields.io/github/stars/coollabsio/coolify?style=flat&label=%E2%98%85&color=F80000) | PaaS self-hosted open-source, alternatif Vercel/Heroku/Netlify. Deploy app & database dengan mudah di VPS Oracle Anda. |
| [Dokploy/dokploy](https://github.com/Dokploy/dokploy) ![](https://img.shields.io/github/stars/Dokploy/dokploy?style=flat&label=%E2%98%85&color=F80000) | Alternatif open-source untuk Vercel, Netlify, dan Heroku. Ringan dan modern. |
| [statickidz/coolify-oci-free](https://github.com/statickidz/coolify-oci-free) ![](https://img.shields.io/github/stars/statickidz/coolify-oci-free?style=flat&label=%E2%98%85&color=F80000) | Deploy Coolify + worker node langsung di Oracle Cloud Free Tier. Siap pakai. |
| [statickidz/dokploy-oci-free](https://github.com/statickidz/dokploy-oci-free) ![](https://img.shields.io/github/stars/statickidz/dokploy-oci-free?style=flat&label=%E2%98%85&color=F80000) | Deploy Dokploy + worker node di Oracle Cloud Free Tier. |

## 🛡️ Networking & Privasi (VPN/Pi-hole)
Manfaatkan bandwidth 10 TB gratis Oracle untuk VPN pribadi & pemblokir iklan.

| Nama | Deskripsi |
|------|-----------|
| [anbuchelva/Pi-hole-and-Wireguard-on-Oracle-Cloud-always-free-tier](https://github.com/anbuchelva/Pi-hole-and-Wireguard-on-Oracle-Cloud-always-free-tier) ![](https://img.shields.io/github/stars/anbuchelva/Pi-hole-and-Wireguard-on-Oracle-Cloud-always-free-tier?style=flat&label=%E2%98%85&color=F80000) | Blokir iklan (Pi-hole) + VPN pribadi (WireGuard) di Oracle Always Free. Panduan lengkap. |

## 📦 Backend & App Self-Hosted
Backend siap pakai yang ringan dan cocok dijalankan di VPS gratis.

| Nama | Deskripsi |
|------|-----------|
| [pocketbase/pocketbase](https://github.com/pocketbase/pocketbase) ![](https://img.shields.io/github/stars/pocketbase/pocketbase?style=flat&label=%E2%98%85&color=F80000) | Backend realtime open-source dalam **1 file executable** (SQLite + Auth + Realtime + Storage). Pasangan sempurna untuk VPS Oracle — tinggal jalankan. |
| [rafaelzimmermann/remote-docker](https://github.com/rafaelzimmermann/remote-docker) ![](https://img.shields.io/github/stars/rafaelzimmermann/remote-docker?style=flat&label=%E2%98%85&color=F80000) | Jalankan Docker secara gratis di Oracle Cloud — konfigurasi remote Docker host. |

## 🏗️ Terraform & IaC
Kelola infrastruktur Oracle gratis Anda sebagai kode (reproducible, versioned).

| Nama | Deskripsi |
|------|-----------|
| [gruberdev/tf-free](https://github.com/gruberdev/tf-free) ![](https://img.shields.io/github/stars/gruberdev/tf-free?style=flat&label=%E2%98%85&color=F80000) `Archived` | Referensi Terraform lintas cloud, termasuk Oracle. Repo read-only; audit dan fork sebelum dipakai. |
| [stealthybox/tf-oci-arm](https://github.com/stealthybox/tf-oci-arm) ![](https://img.shields.io/github/stars/stealthybox/tf-oci-arm?style=flat&label=%E2%98%85&color=F80000) | Terraform yang dapat dikonfigurasi untuk VM ARM Ubuntu gratis di Oracle dengan firewall. |

## 📚 Referensi & Panduan
Sumber belajar untuk memaksimalkan Oracle Free Tier.

| Nama | Deskripsi |
|------|-----------|
| [neitsab/awesome-oracle-cloud-free-tier](https://github.com/neitsab/awesome-oracle-cloud-free-tier) ![](https://img.shields.io/github/stars/neitsab/awesome-oracle-cloud-free-tier?style=flat&label=%E2%98%85&color=F80000) | *Awesome-list* rujukan utama (berbahasa Inggris) untuk memanfaatkan Oracle Cloud Free Tier secara maksimal. |
| [1999AZZAR/oci-always-free-course](https://github.com/1999AZZAR/oci-always-free-course) ![](https://img.shields.io/github/stars/1999AZZAR/oci-always-free-course?style=flat&label=%E2%98%85&color=F80000) | 🇮🇩 Panduan lengkap (berbahasa Indonesia) memanfaatkan OCI Always Free: provisioning ARM Ampere A1 dan lainnya. |
| [brucethemoose/Free-Oracle-Minecraft-Server-Tutorial](https://github.com/brucethemoose/Free-Oracle-Minecraft-Server-Tutorial) ![](https://img.shields.io/github/stars/brucethemoose/Free-Oracle-Minecraft-Server-Tutorial?style=flat&label=%E2%98%85&color=F80000) | Tutorial komunitas menjalankan server Minecraft di Oracle Free Tier. Verifikasi kebutuhan resource dan kebijakan terbaru sebelum digunakan. |

## 📄 Tips Cepat

### 1. Melawan "Out of Capacity" ARM
Region ramai (Singapore, dll) sering kehabisan kapasitas ARM. Solusi:
- Gunakan **script auto-retry** (lihat kategori pertama) — ia mencoba tiap beberapa menit sampai dapat.
- Alokasikan VM ARM sesuai limit yang tampil di tenancy; konfigurasi lebih kecil kadang lebih mudah mendapat kapasitas.
- Pilih **region yang tidak terlalu ramai** saat mendaftar (region tidak bisa diubah setelahnya).

### 2. Buka Port (Firewall 2 Lapis!)
Oracle punya 2 firewall — sering bikin pemula bingung kenapa port tak bisa diakses:
```bash
# Lapis 1: Security List / NSG di Oracle Console (tambah Ingress Rule untuk port Anda)
# Lapis 2: iptables DI DALAM VM (Ubuntu Oracle punya rule ketat bawaan). Contoh buka port 80:
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 80 -j ACCEPT
sudo netfilter-persistent save
```

### 3. Reclaim & Kebijakan Penggunaan
Oracle dapat mengambil kembali resource idle sesuai kebijakan layanan. Jalankan **workload nyata**, pantau notifikasi akun, dan siapkan backup. Jangan membuat trafik atau beban palsu untuk mengakali kebijakan reclaim.

---

## 🤝 Kontribusi
Menemukan script atau panduan Oracle Free menarik lainnya? Silakan buat *Pull Request*! Baca dulu [panduan kontribusi](CONTRIBUTING.md).

<a href="https://github.com/ridloabelian/awesome-oracle-free-id/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=ridloabelian/awesome-oracle-free-id" alt="Contributors" />
</a>

## 📜 Lisensi
Lisensi MIT - [Ridlo Abelian](https://github.com/ridloabelian)

---

<div align="center">

<a href="#kitab-oracle-cloud--">⬆️ Kembali ke Atas</a>

</div>
