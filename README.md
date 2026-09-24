# 🕌 waqf-odoo-modules

> **Kumpulan Modul Ekstensi Resmi Odoo 19 & 18 Community Edition untuk Tata Kelola & Akuntansi Wakaf Nasional (PSAK 412/112 & LSP BWI)**  
> Inisiatif kolaboratif **Forum Wakaf Produktif (FWP / [fwp.or.id](https://fwp.or.id))** bersama **Asosiasi Nazhir Indonesia (ANI / [ani.or.id](https://ani.or.id))**, diinisiasi & dikembangkan oleh **Amal Produktif ([amalproduktif.or.id](https://amalproduktif.or.id))** untuk kemandirian, transparansi, dan digitalisasi tata kelola Nazhir di seluruh Indonesia.

[![Odoo Version](https://img.shields.io/badge/Odoo-19.0%20%7C%2018.0%20(LTS)-714B67?logo=odoo&logoColor=white)](https://www.odoo.com)
[![Standard](https://img.shields.io/badge/Standard-OCA%20Compliant-brightgreen.svg)](https://odoo-community.org/)
[![Accounting Standard](https://img.shields.io/badge/Accounting-PSAK%20412%20(112)%20IAI-059669)](https://web.iaiglobal.or.id/)
[![Competency Standard](https://img.shields.io/badge/Certification-LSP%20BWI%20%7C%20BNSP-blue)](https://www.bwi.go.id)
[![Collaboration](https://img.shields.io/badge/Initiative-FWP%20%C3%97%20ANI-008080)](https://fwp.or.id)
[![Developer: Amal Produktif](https://img.shields.io/badge/Lead%20Nazhir-Amal%20Produktif-16a34a.svg)](https://amalproduktif.or.id)
[![License: LGPL-3](https://img.shields.io/badge/License-LGPL--3.0-blue.svg)](LICENSE)

---

## 📌 1. Latar Belakang & Visi Proyek

Tata kelola wakaf di Indonesia memasuki era baru yang menuntut akuntabilitas publik tinggi. Sistem ini dirancang untuk menjadi standar terbuka (*open-source standard*) tata kelola digital wakaf yang siap digunakan oleh seluruh Nazhir di Indonesia (pesantren, yayasan, BKM masjid, lembaga filantropi Islam, hingga nazhir institusi/BUMN).

Sistem ini dirancang untuk patuh dan selaras dengan 3 pilar:
1. **Regulasi UU No. 41 Tahun 2004 tentang Wakaf** beserta PP No. 42 Tahun 2006 dan Peraturan Badan Wakaf Indonesia (BWI).
2. **Standar Akuntansi Keuangan Syariah PSAK 412 (sebelumnya PSAK 112: Akuntansi Wakaf)** yang diterbitkan oleh Ikatan Akuntan Indonesia (IAI).
3. **10 Skema Standar Kompetensi Kerja Nasional Indonesia (SKKNI) LSP BWI** (dari skema SS.001 sampai SS.010).

---

## 🛡️ 2. Batasan Arsitektur Krusial (GUARDRAILS)

- **100% Modul Ekstensi (Custom Add-ons)**: DILARANG keras mem-fork core Odoo! Modul berjalan murni di atas Odoo 19.0 & 18.0 Community Edition resmi.
- **Standar OCA (Odoo Community Association)**: Seluruh struktur folder, manifest, naming conventions, dan lisensi mematuhi pedoman OCA.
- **Engine Pelaporan Modern (`account.report`)**: Menggunakan engine pelaporan modern Odoo (`account.report`, `account.report.column`, `account.report.line`, `account.report.expression`).
- **Antarmuka Reaktif OWL (Odoo Web Library)**: Menggunakan sintaks OWL terbaru untuk dashboard pelaporan interaktif.
- **Lisensi Kode**: LGPL-3.0 (GNU Lesser General Public License v3.0).

---

## 🧩 3. Daftar Modul dalam Repositori

| Modul | Status | Deskripsi Utama |
| :--- | :--- | :--- |
| [`waqf_core`](waqf_core/) | ✅ Siap Pakai | **Modul Inti & Operasional**: Master data Wakif (KYC, NIK 16 digit, NPWP/NIB), pencatatan Akta Ikrar Wakaf (AIW/APAIW), alur verifikasi standar BWI (*Draft -> Verified Legal -> Approved Nazhir -> Issued*), dan cetak Sertifikat Wakaf resmi berstandar BWI (QWeb PDF). |
| [`l10n_id_waqf_psak112`](l10n_id_waqf_psak112/) | ✅ Siap Pakai | **Akuntansi Syariah PSAK 412 (112)**: Bagan Akun Standar (COA), Klasifikasi Aset Neto (Permanen, Temporer, Tidak Terikat), Validasi Syariah dana pokok abadi haram berkurang/disalurkan, Batasan hak operasional Nazhir maks 10% (UU 41/2004 Ps. 12), Dashboard Interaktif OWL, dan 4 Laporan Keuangan Wajib PSAK 412/112. |
| [`waqf_distribution`](waqf_distribution/) | ✅ Siap Pakai | **Penyaluran Manfaat**: Master data Mauquf 'Alaih (Individu/Lembaga), Asesmen kelayakan syariah, Program pendayagunaan, Otomasi entri jurnal beban PSAK 412 (Aset Neto Tidak Terikat), Proteksi syariah dana pokok abadi haram disalurkan, dan Dokumen BAST/Kuitansi Standar BWI (QWeb PDF). |
| `waqf_asset_management` | 🔜 Tahap Berikutnya | **Penjagaan Aset Abadi**: Pencatatan aset tanah & fisik wakaf, status sertifikat BPN, status asuransi syariah, dan log inspeksi pemeliharaan rutin. |

---

## ⚖️ 4. Ketentuan Syariah & Regulasi yang Ditanamkan

### A. Aturan Syariah Pokok Wakaf Permanen (`@api.constrains`)
Sesuai PSAK 412 (112) Paragraf 26-28 dan UU No. 41/2004 Pasal 40:
- Pokok wakaf permanen diakui sebagai **Aset Neto Terikat Permanen**.
- Sistem secara otomatis membatalkan dan melempar `ValidationError` jika ada entri jurnal yang mendebit/mengurangi pokok wakaf permanen untuk membiayai beban operasional atau beban penyaluran Mauquf 'Alaih.
- Penyaluran manfaat kepada Mauquf 'Alaih **HANYA** boleh dibiayai dari **Aset Neto Tidak Terikat (Surplus Bersih Hasil Pengelolaan & Pengembangan)**.

### B. Batasan Hak Nazhir Maksimal 10% (UU 41/2004 Pasal 12)
- Sistem menghitung otomatis Hasil Bersih Pengelolaan:
  $$\text{Hasil Bersih} = \text{Pendapatan Kotor Pengelolaan} - \text{Beban Pemeliharaan Langsung}$$
- Membatasi hak operasional nazhir maksimal **10% dari hasil bersih**. Jika melebihi atau hasil bersih defisit, sistem otomatis menolak transaksi.
- Otomasi pembentukan entri jurnal pengakuan hak nazhir saat diverifikasi.

### C. Penyaluran Mauquf 'Alaih & BAST Standar BWI
- Sesuai UU No. 41/2004 Pasal 22-23: Penyaluran terbagi ke sektor Pendidikan, Kesehatan, Ekonomi UMKM, Dakwah & Sarana Ibadah, serta Kemanusiaan.
- Asesmen kelayakan mustahiq (Eligible) wajib terpenuhi sebelum persetujuan komite.
- Otomasi pembentukan entri jurnal akuntansi beban penyaluran (`530100`) vs kas/bank saat realisasi disalurkan.
- Pencetakan resmi Berita Acara Serah Terima (BAST) & Tanda Terima Manfaat Wakaf 3 pihak (Penerima, Staf Program, Pimpinan Nazhir).

### D. 4 Laporan Keuangan Wajib PSAK 412 (112)
1. **Laporan Posisi Keuangan (Neraca)**
2. **Laporan Rincian Aset Wakaf**
3. **Laporan Aktivitas**
4. **Laporan Arus Kas**

---

## 🚀 5. Panduan Instalasi Modul di Odoo Anda

Jika Anda sudah memiliki instalasi Odoo 19.0 atau 18.0 yang berjalan:

### Langkah 1: Kloning Repositori
Masuk ke direktori custom add-ons Odoo Anda:
```bash
cd /path/to/odoo/custom-addons
git clone https://github.com/ridloabelian/waqf-odoo-modules.git -b 19.0
```

### Langkah 2: Tambahkan ke `addons_path`
Pastikan direktori repositori terdaftar pada file konfigurasi Odoo (`odoo.conf`):
```ini
addons_path = /path/to/odoo/addons,/path/to/odoo/custom-addons/waqf-odoo-modules
```
Restart service Odoo Anda.

### Langkah 3: Aktivasi di Odoo Web UI
1. Masuk ke Odoo sebagai **Administrator**.
2. Buka **Settings** ➔ Gulir ke bawah ➔ Klik **Activate the developer mode**.
3. Buka menu **Apps** (Aplikasi).
4. Klik tombol **Update Apps List** pada bilah navigasi atas, lalu konfirmasi.
5. Hapus filter default `"Apps"` di kotak pencarian, lalu ketik `waqf` atau `psak`.
6. Klik tombol **Activate / Install** pada modul:
   - `Tata Kelola Wakaf - Core & Operasional` (`waqf_core`)
   - `Akuntansi Wakaf PSAK 412 (PSAK 112) & Regulasi UU 41/2004` (`l10n_id_waqf_psak112`)
   - `Penyaluran Manfaat Wakaf - Mauquf 'Alaih & Program Sosial` (`waqf_distribution`)

---

## 🐳 Paket Turnkey 1-Klik (Docker)

Bagi lembaga Nazhir atau tim IT yang ingin men-deploy server Odoo Wakaf lengkap siap pakai (termasuk Caddy Reverse Proxy, Auto-SSL HTTPS, PostgreSQL 17/16, dan otomasi backup harian) hanya dalam 5 menit, silakan gunakan paket instalasi turnkey kami:

👉 **[waqf-odoo-docker (Paket Turnkey VPS 1-Klik)](https://github.com/ridloabelian/waqf-odoo-docker)**

---

## 🏛️ Inisiator & Kolaborator Proyek

Proyek standardisasi digitalisasi tata kelola dan akuntansi wakaf ini diinisiasi dan dikembangkan secara kolaboratif oleh:
- **[Amal Produktif](https://amalproduktif.or.id)** – Lembaga Nazhir Wakaf Produktif terdaftar & *Lead Technical Maintainer* ekosistem modul.
- **[Forum Wakaf Produktif (FWP)](https://fwp.or.id)** – Wadah kolaborasi dan inkubasi tata kelola wakaf produktif nasional.
- **[Asosiasi Nazhir Indonesia (ANI)](https://ani.or.id)** – Asosiasi resmi penghimpun profesi dan kelembagaan Nazhir di seluruh Indonesia.

Didukung oleh standardisasi kompetensi & regulasi:
- **LSP Badan Wakaf Indonesia (BWI)** – Standar Kompetensi Kerja Nasional Indonesia (SKKNI) Nazhir SS.001 - SS.010.
- **Dewan Standar Akuntansi Syariah (DSAS) IAI** – PSAK 412 (sebelumnya PSAK 112: Akuntansi Wakaf).

---

## 👥 Kontribusi & Lisensi

Proyek ini berada di bawah lisensi resmi [LGPL-3.0](LICENSE). 

Kontribusi terbuka luas untuk seluruh pegiat wakaf, asosiasi nazhir, akuntan syariah, dan pengembang Odoo di seluruh Indonesia. Silakan buat *Issue* atau ajukan *Pull Request* mengikuti [Panduan Kontribusi](.github/pull_request_template.md).

