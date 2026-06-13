# 📓 Laporan Harian

Aplikasi pencatatan harian pembelajaran anak — single-file HTML, bisa diinstall di HP sebagai Progressive Web App (PWA).

Dibuat untuk mencatat laporan harian homeschooling: topik, proses/anekdot, rating Enjoy & Easy per mata pelajaran, lalu langsung kirim ke Google Sheets dan salin ke Telegram.

---

## ✨ Fitur

### Profil Anak (multi-anak)
- Setiap anak punya profil sendiri: nama, kelas aktif, semester (1/2), dan daftar mata pelajaran
- Bisa tambah anak baru, edit, atau hapus profil
- Profile bar di bawah header — klik untuk beralih antar anak
- Bisa tambah kelas baru dan mata pelajaran baru
- **Satu anak = satu Google Sheets** (URL tersimpan per profil)
- Semua data tersimpan di `localStorage` browser

### Entry Harian
- Pilih tanggal (kalender) dan semester
- Pilih mata pelajaran dari dropdown — hanya mapel aktif di profil yang muncul
- Isi topik/judul, proses/anekdot, rating Enjoy (1–5) dan Easy (1–5), upload foto
- Tombol **+** untuk tambah mata pelajaran kedua, ketiga, dst.
- Tombol hapus per blok mata pelajaran

### Output Telegram
- Tombol **Salin Teks** menyalin teks berformat langsung ke clipboard
- Format: tanggal *italic*, nama mapel **bold**, proses/anekdot *italic*, Enjoy/Easy **bold**
- Pratinjau terformat muncul di aplikasi sebelum disalin
- Kompatibel dengan Telegram Desktop dan Telegram Web

### Google Sheets
- Tombol **Kirim ke Sheets** mengirim data ke Google Sheets via Apps Script Web App
- Tab baru dibuat otomatis jika mata pelajaran belum ada
- Header otomatis: **Kelas | Semester | Sesi | Tanggal | Judul | Proses/Anekdot | Enjoy | Easy**
- Header berwarna teal, kolom Proses/Anekdot otomatis wrap text
- Nomor sesi dihitung otomatis dari jumlah baris yang sudah ada

### PWA (Progressive Web App)
- Bisa diinstall di layar utama HP Android (Chrome) dan iOS (Safari)
- Tampil fullscreen tanpa browser bar setelah diinstall
- Service Worker untuk caching offline

---

## 📁 File di Repo

| File | Keterangan |
|------|------------|
| `index.html` | Aplikasi utama (single-file, semua fitur di sini) |
| `sw.js` | Service Worker untuk PWA offline caching |
| `README.md` | Dokumentasi ini |

---

## 🚀 Cara Pakai

### Opsi A — Langsung buka di browser (tanpa install)
1. Download `index.html` dan `sw.js` ke folder yang sama
2. Buka `index.html` di browser

> ⚠️ Service Worker tidak aktif saat dibuka via `file://`. Semua fitur lain tetap berjalan normal.

### Opsi B — GitHub Pages (direkomendasikan, PWA penuh)
1. Fork atau clone repo ini
2. Aktifkan GitHub Pages: **Settings → Pages → Branch: main → / (root) → Save**
3. Buka URL: `https://[username].github.io/[nama-repo]`
4. Di Chrome Android: tunggu banner **"Install Laporan Harian"** muncul → tap **Install**
5. Di iOS Safari: **Share → Add to Home Screen**

---

## ⚙️ Setup Google Sheets (per anak, sekali saja)

### 1. Buat Google Sheets baru
Buka [sheets.google.com](https://sheets.google.com) → buat spreadsheet baru, beri nama misalnya `Laporan Harian`.

### 2. Buka Apps Script
**Extensions → Apps Script** → hapus kode default.

### 3. Paste kode Apps Script
Di aplikasi, klik **⚙ Hubungkan Sheets** di header → **Salin Kode Apps Script** → paste ke Apps Script → Save.

### 4. Deploy sebagai Web App
**Deploy → New deployment → Web app**
- Execute as: **Me**
- Who has access: **Anyone**

Klik **Deploy** → izinkan akses → copy **URL Web App**.

### 5. Sambungkan ke profil anak
Di aplikasi: klik nama anak di profile bar → **Edit Profil** → scroll ke bawah → paste URL di field **Google Sheets** → **Simpan Profil**.

Badge di header akan berubah menjadi **"Sheets Terhubung" ✅**

> Untuk anak kedua, ulangi seluruh langkah dengan Sheets baru.

---

## 📊 Format Google Sheets

Setiap mata pelajaran mendapat satu tab tersendiri. Tab dibuat otomatis dengan format:

| Kelas | Semester | Sesi | Tanggal | Judul | Proses/Anekdot | Enjoy | Easy |
|-------|----------|------|---------|-------|----------------|-------|------|
| Kelas 3 | Semester 2 | 1 | 14 Juni 2026 | Bilangan bulat | A langsung paham... | 5 | 4 |

---

## 📚 Daftar Mata Pelajaran Default (20)

Al-Quran, Adab, Matematika, Bahasa Arab, Literasi, Siroh, PPKN, Ibadah, Olahraga, Life Skill, White Bee Hero, Program Khas, Kelas Inspirasi, Outing, Bahasa Inggris, Bahasa Indonesia, Rumah Peradaban, Petani Cilik, Peternak Cilik, Pedagang Cilik

Mata pelajaran baru bisa ditambahkan langsung dari modal profil.

---

## 🛠️ Teknologi

- **HTML + CSS + JavaScript** murni — tanpa framework, tanpa build step
- **localStorage** untuk penyimpanan data profil dan konfigurasi
- **Web App Manifest** (blob URL) untuk metadata PWA
- **Service Worker** (`sw.js`) untuk offline caching
- **Google Apps Script** untuk integrasi Google Sheets
- Font: [Lora](https://fonts.google.com/specimen/Lora) + [Nunito](https://fonts.google.com/specimen/Nunito)

---

## 📝 Catatan Pengembangan

### Versi
| Versi | Perubahan |
|-------|-----------|
| v1 | Versi awal — entry harian, output Telegram, Google Sheets, multi-profil |
| v2 | PWA: manifest + install banner + SW (blob — kemudian diganti) |
| v3 | SW dipindah ke `sw.js` eksternal, manifest tetap inline |
| v4 | GSheet URL per profil anak, Apps Script dengan format header |

### Keterbatasan
- Service Worker hanya aktif di `https://` — tidak aktif saat dibuka via `file://`
- `beforeinstallprompt` (install banner otomatis) hanya di Chrome Android; iOS perlu manual via Share
- Foto yang diupload tidak dikirim ke Google Sheets (hanya tersimpan lokal di pratinjau)
- Tidak ada sinkronisasi dua arah dengan GSheet — data hanya mengalir dari app ke Sheets

---

*Dibuat dengan ❤️ untuk mendokumentasikan perjalanan belajar Kinan.*
