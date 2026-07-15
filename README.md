<div align="center">

<img src="https://upload.wikimedia.org/wikipedia/commons/5/50/Oracle_logo.svg" alt="Oracle Logo" width="240" />

<h1 align="center">Kitab Oracle Cloud 🗄️ 🇮🇩<br><sub>(VPS Gratis Selamanya)</sub></h1>

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=500&size=20&pause=1000&color=F80000&center=true&vCenter=true&width=680&lines=4+Core+ARM+%2B+24GB+RAM+GRATIS;Bukan+Trial%2C+Tapi+Always+Free;VPS+Sungguhan+Untuk+Docker;Bangun+Server+Modal+Rp+0" alt="Typing SVG" />
</p>

Kumpulan panduan, *script* automasi, dan proyek *open-source* untuk memanfaatkan **Oracle Cloud Always Free Tier** — satu-satunya penyedia cloud yang memberikan **VPS sungguhan gratis selamanya** (bukan trial): hingga **4 core ARM Ampere + 24 GB RAM**.
Dibangun untuk developer & *indie hacker* Indonesia yang butuh server beneran (Docker, database, self-hosting) dengan biaya Rp 0.

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![Stars](https://img.shields.io/github/stars/ridloabelian/awesome-oracle-free-id?style=flat&color=F80000)](https://github.com/ridloabelian/awesome-oracle-free-id/stargazers)
[![Last Commit](https://img.shields.io/github/last-commit/ridloabelian/awesome-oracle-free-id?style=flat&color=F80000)](https://github.com/ridloabelian/awesome-oracle-free-id/commits/main)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat)](CONTRIBUTING.md)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](LICENSE)

</div>

> 🔗 **Seri saudara:** [**Cloudflare**](https://github.com/ridloabelian/awesome-cloudflare-id) (edge) · [**Google**](https://github.com/ridloabelian/awesome-google-free-id) (automasi) · [**Supabase**](https://github.com/ridloabelian/awesome-supabase-id) (database) · [**Telegram**](https://github.com/ridloabelian/awesome-telegram-infra-id) (infra chat). **Oracle melengkapi seri sebagai satu-satunya VPS/compute penuh gratis — untuk beban yang tak muat di serverless (Docker, DB berat, game server, self-hosting).**

Berbeda dari yang lain di seri ini yang berbasis *serverless*, Oracle Cloud memberi Anda **komputer Linux beneran** yang bisa di-SSH, jalankan Docker, database, atau apa pun — dan itu **gratis permanen** (Always Free, tanpa batas waktu). Ini "cheat code" untuk yang butuh kontrol penuh tanpa bayar VPS bulanan.

**Kriteria Kurasi:**
- Memanfaatkan Oracle Cloud Always Free (permanen, bukan trial 30 hari).
- Automasi *provisioning*, self-hosting, atau IaC (Terraform/script).
- *Open-source* dan idealnya masih aktif di-*maintain*.
- Bermanfaat untuk developer & solopreneur Indonesia.

---

## 💰 Apa Saja yang GRATIS Selamanya di Oracle?

| Sumber Daya | Batas Always Free | Catatan |
|-------------|-------------------|---------|
| **ARM Ampere A1** | 4 vCPU + 24 GB RAM (bisa dibagi jadi beberapa VM) | ⭐ Bintang utama. Setara VPS berbayar ~$30/bln. |
| **VM AMD (x86)** | 2× VM (1 vCPU + 1 GB RAM masing-masing) | Untuk beban ringan / kompatibilitas x86. |
| **Block Storage** | 200 GB total | Untuk disk VM. |
| **Object Storage** | 20 GB (10 GB standard + 10 GB archive) | Mirip S3. |
| **Bandwidth keluar** | 10 TB/bulan | Sangat besar, cukup untuk banyak layanan. |
| **Load Balancer** | 1 (10 Mbps) | Gratis. |
| **Database Otonom** | 2× (20 GB masing-masing) | Oracle Autonomous DB. |

> ⚠️ **Penting & jujur:** (1) **Kartu kredit/debit diperlukan** untuk verifikasi saat daftar (tidak ditagih untuk Always Free). (2) Kapasitas ARM sering **"Out of Capacity"** di region ramai — makanya banyak *script* auto-retry di repo ini. (3) Instance yang benar-benar *idle* bisa di-*reclaim*; jaga tetap ada aktivitas. (4) Pilih region yang tepat saat daftar (tidak bisa diubah).

---

## Daftar Isi
- [💰 Apa Saja yang GRATIS Selamanya di Oracle?](#-apa-saja-yang-gratis-selamanya-di-oracle)
- [🎯 Auto-Provisioning ARM (Anti "Out of Capacity")](#-auto-provisioning-arm-anti-out-of-capacity)
- [☸️ Kubernetes (k3s/k8s) Gratis](#️-kubernetes-k3sk8s-gratis)
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

## ☸️ Kubernetes (k3s/k8s) Gratis
Jalankan cluster Kubernetes lengkap di atas 4 core ARM gratis — untuk belajar atau produksi kecil.

| Nama | Deskripsi |
|------|-----------|
| [garutilorenzo/k3s-oci-cluster](https://github.com/garutilorenzo/k3s-oci-cluster) ![](https://img.shields.io/github/stars/garutilorenzo/k3s-oci-cluster?style=flat&label=%E2%98%85&color=F80000) | Deploy cluster Kubernetes (k3s) gratis penuh menggunakan Terraform di Oracle Always Free. Lengkap & terawat. |
| [nce/oci-free-cloud-k8s](https://github.com/nce/oci-free-cloud-k8s) ![](https://img.shields.io/github/stars/nce/oci-free-cloud-k8s?style=flat&label=%E2%98%85&color=F80000) | Panduan & IaC untuk menjalankan Kubernetes gratis selamanya di Oracle Cloud. |
| [r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure](https://github.com/r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure) ![](https://img.shields.io/github/stars/r0b2g1t/k3s-cluster-on-oracle-cloud-infrastructure?style=flat&label=%E2%98%85&color=F80000) | Deploy cluster k3s otomatis penuh, termasuk Infrastructure as Code. |

## 🚀 PaaS Self-Hosted (Vercel/Heroku Alternative)
Punya "Vercel/Heroku" sendiri di VPS gratis — deploy app dengan git push, gratis selamanya.

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
| [gruberdev/tf-free](https://github.com/gruberdev/tf-free) ![](https://img.shields.io/github/stars/gruberdev/tf-free?style=flat&label=%E2%98%85&color=F80000) | Terraform untuk membuat sumber daya gratis di berbagai penyedia cloud besar, termasuk Oracle. |
| [stealthybox/tf-oci-arm](https://github.com/stealthybox/tf-oci-arm) ![](https://img.shields.io/github/stars/stealthybox/tf-oci-arm?style=flat&label=%E2%98%85&color=F80000) | Terraform yang dapat dikonfigurasi untuk VM ARM Ubuntu gratis di Oracle dengan firewall. |

## 📚 Referensi & Panduan
Sumber belajar untuk memaksimalkan Oracle Free Tier.

| Nama | Deskripsi |
|------|-----------|
| [neitsab/awesome-oracle-cloud-free-tier](https://github.com/neitsab/awesome-oracle-cloud-free-tier) ![](https://img.shields.io/github/stars/neitsab/awesome-oracle-cloud-free-tier?style=flat&label=%E2%98%85&color=F80000) | *Awesome-list* rujukan utama (berbahasa Inggris) untuk memanfaatkan Oracle Cloud Free Tier secara maksimal. |
| [1999AZZAR/oci-always-free-course](https://github.com/1999AZZAR/oci-always-free-course) ![](https://img.shields.io/github/stars/1999AZZAR/oci-always-free-course?style=flat&label=%E2%98%85&color=F80000) | 🇮🇩 Panduan lengkap (berbahasa Indonesia) memanfaatkan OCI Always Free: provisioning ARM Ampere A1 dan lainnya. |
| [brucethemoose/Free-Oracle-Minecraft-Server-Tutorial](https://github.com/brucethemoose/Free-Oracle-Minecraft-Server-Tutorial) ![](https://img.shields.io/github/stars/brucethemoose/Free-Oracle-Minecraft-Server-Tutorial?style=flat&label=%E2%98%85&color=F80000) | Tutorial menjalankan server Minecraft gratis di 4-core/24GB ARM Oracle. Contoh nyata kekuatan free tier. |

## 📄 Tips Cepat

### 1. Melawan "Out of Capacity" ARM
Region ramai (Singapore, dll) sering kehabisan kapasitas ARM. Solusi:
- Gunakan **script auto-retry** (lihat kategori pertama) — ia mencoba tiap beberapa menit sampai dapat.
- Coba **buat 1 VM ARM sekaligus 4 OCPU/24GB** (lebih susah dapat) ATAU pecah jadi VM kecil (lebih mudah dapat slot).
- Pilih **region yang tidak terlalu ramai** saat mendaftar (region tidak bisa diubah setelahnya).

### 2. Buka Port (Firewall 2 Lapis!)
Oracle punya 2 firewall — sering bikin pemula bingung kenapa port tak bisa diakses:
```bash
# Lapis 1: Security List / NSG di Oracle Console (tambah Ingress Rule untuk port Anda)
# Lapis 2: iptables DI DALAM VM (Ubuntu Oracle punya rule ketat bawaan). Contoh buka port 80:
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 80 -j ACCEPT
sudo netfilter-persistent save
```

### 3. Cegah Instance Di-reclaim (jaga tetap "aktif")
Oracle bisa mengambil kembali instance yang benar-benar idle. Pastikan ada beban ringan:
```bash
# Contoh: cron ringan tiap 5 menit agar CPU tidak 0% terus (jangan berlebihan)
# crontab -e
*/5 * * * * /usr/bin/uptime > /dev/null 2>&1
```

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
