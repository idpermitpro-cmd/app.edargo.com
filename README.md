# EdarGo ERP System

**Full-stack internal ERP** untuk EdarGo Academy & Consulting.  
Frontend: Cloudflare Pages (single `index.html`) — Backend: Google Apps Script + Google Sheets

---

## 🚀 Deploy dalam 5 Menit

### Step 1 — Google Sheet
1. Buka [Google Sheets](https://sheets.google.com) → buat sheet baru
2. Copy **Sheet ID** dari URL: `https://docs.google.com/spreadsheets/d/**[SHEET_ID]**/edit`

### Step 2 — Google Apps Script
1. Buka [script.google.com](https://script.google.com) → **New Project**
2. Beri nama: `EdarGo ERP API`
3. Hapus kode default, paste isi file **`apps-script.gs`**
4. Isi `SHEET_ID` di baris pertama dengan ID dari Step 1
5. Klik **Deploy → New Deployment**
   - Type: **Web App**
   - Execute as: **Me**
   - Who has access: **Anyone**
6. Klik **Deploy** → Copy URL yang muncul (format: `https://script.google.com/macros/s/xxx/exec`)
7. Jalankan fungsi `setupSheets()` sekali untuk inisialisasi kolom

### Step 3 — Cloudflare Pages
1. Push file `index.html` ke GitHub repository baru
2. Buka [Cloudflare Pages](https://pages.cloudflare.com) → **Create a project**
3. Connect ke GitHub repository
4. Build settings: **No build required** (Framework: None)
5. Deploy → Cloudflare akan memberikan URL seperti `edargo-erp.pages.dev`

### Step 4 — Custom Domain (opsional)
Di Cloudflare DNS, tambahkan record:
```
Type: CNAME
Name: app
Target: edargo-erp.pages.dev
```
ERP akan bisa diakses di `app.edargo.com`

### Step 5 — Konfigurasi ERP
1. Buka ERP di browser
2. Klik **Pengaturan** (sidebar kiri bawah)
3. Tempel **Apps Script URL** dari Step 2
4. Tempel **Google Sheet ID** dari Step 1
5. Klik **Simpan Konfigurasi** → **Test Koneksi**

---

## 📋 Modul ERP

| Modul | Fitur |
|-------|-------|
| **Dashboard** | KPI cards, pipeline chart, aktivitas terbaru |
| **Klien (CRM)** | CRUD klien, filter status & jenis izin |
| **Proyek** | Tracking 7-tahap, List & Board view, advance step |
| **Dokumen** | Checklist per proyek, status per dokumen |
| **Tagihan** | Invoice CRUD, ubah status, revenue summary |
| **Tim** | Beban kerja anggota, skill tag |
| **Laporan** | Analitik, export ke Google Sheets |
| **Pengaturan** | GAS URL, Sheet ID, DNS guide, backup JSON |

---

## ⚙️ Arsitektur

```
Browser (app.edargo.com)
        │
        ▼
Cloudflare Pages
  └── index.html (React 18 + Chart.js via CDN)
        │  localStorage (state lokal)
        │
        ▼
Google Apps Script Web App (api.edargo.com)
  └── apps-script.gs
        │
        ▼
Google Sheets (database)
  ├── Klien
  ├── Proyek
  ├── Tagihan
  ├── Tim
  └── Log Aktivitas
```

---

## 🛠 Tech Stack
- **React 18** via CDN (unpkg.com) — no build step
- **Babel Standalone** — JSX transpilation in browser
- **Chart.js 4** — Dashboard charts
- **Google Apps Script** — Serverless backend
- **Google Sheets** — Database
- **Cloudflare Pages** — Static hosting

---

## 📁 File Structure
```
edargo-erp/
├── index.html       ← Upload ke Cloudflare Pages
├── apps-script.gs   ← Paste ke Google Apps Script
└── README.md        ← Panduan ini
```

---

## 🔒 Catatan Keamanan
- ERP ini untuk **internal use only** — tidak ada autentikasi bawaan
- Tambahkan password protection di Cloudflare Pages jika diperlukan
- Apps Script URL sebaiknya hanya dibagikan ke tim internal
- Backup data secara rutin via **Pengaturan → Export JSON**

---

## 📞 Support
EdarGo Academy & Consulting  
info@edargo.com | wa.me/62XXXXXXXXXX
