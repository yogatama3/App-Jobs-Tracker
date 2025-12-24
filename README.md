## Deskripsi Proyek
JobTrackPro adalah aplikasi web berbasis pelacakan lamaran pekerjaan yang dirancang untuk membantu pencari kerja memantau progres aplikasi pekerjaan mereka. Aplikasi ini memungkinkan pengguna untuk mencatat lamaran pekerjaan, melacak statusnya, dan mengelola akun pengguna dengan fitur admin. Backend aplikasi menggunakan Google Apps Script yang terintegrasi dengan Google Sheets untuk penyimpanan data, sementara frontend dibangun dengan HTML, CSS (Bootstrap), dan JavaScript untuk antarmuka yang responsif dan user-friendly.

Aplikasi ini cocok untuk individu atau tim kecil yang ingin mengorganisir proses pencarian kerja secara efisien, dengan fitur seperti dashboard statistik, pencarian dan filter data, serta pembaruan status lamaran dengan catatan khusus (misalnya, alasan penolakan atau detail wawancara).

## Fitur Utama
- **Autentikasi Pengguna**: Login dengan email dan password yang di-hash untuk keamanan.
- **Dashboard Statistik**: Tampilan kartu statistik seperti total lamaran, lamaran aktif, jumlah wawancara, dan tingkat keberhasilan.
- **Form Tambah Lamaran**: Input data lamaran baru (perusahaan, posisi, lokasi, tanggal, media, dll.).
- **Riwayat Lamaran**: 
  - Tampilan tabel untuk desktop.
  - Tampilan kartu untuk mobile.
- **Pembaruan Status**: Edit status lamaran (Applied, Interviewing, Approve!, Decline, dll.) dengan catatan yang disesuaikan berdasarkan status.
- **Pencarian dan Filter**: Cari berdasarkan perusahaan/posisi, filter berdasarkan status atau hasil.
- **Panel Admin**: Kelola pengguna (tambah, edit, hapus) untuk admin.
- **Pengaturan Pengguna**: Ubah password.
- **Responsif**: Desain yang mendukung desktop dan mobile.
- **Auto-Login**: Simpan sesi login menggunakan localStorage.

## Teknologi yang Digunakan
- **Frontend**: HTML5, CSS3 (Bootstrap 5.3.0), JavaScript (ES6+).
- **Backend**: Google Apps Script (GAS) untuk logika server-side.
- **Penyimpanan Data**: Google Sheets (Spreadsheet) dengan dua sheet utama: "Lamaran" dan "Users".
- **Keamanan**: Hashing password menggunakan SHA-256 dengan salt.
- **Library Eksternal**: Bootstrap untuk styling, Bootstrap Icons untuk ikon.

## Prasyarat
- Akun Google dengan akses ke Google Sheets dan Google Apps Script.
- Pengetahuan dasar tentang HTML, CSS, JavaScript, dan Google Apps Script.
- Browser web modern (Chrome, Firefox, Safari) yang mendukung JavaScript.
- Akses internet untuk memuat CDN Bootstrap dan menjalankan GAS.

## Instalasi dan Setup
Ikuti langkah-langkah berikut untuk mengatur JobTrackPro dari awal:

### 1. Buat Google Spreadsheet
- Buka Google Sheets dan buat spreadsheet baru.
- Tambahkan dua sheet: "Lamaran" dan "Users".
- **Sheet "Lamaran"**:
  - Mulai dari baris 7: Kolom A (No), B (Perusahaan), C (Posisi), D (Lokasi), E (Tanggal), F (Media), G (Status - dengan rumus), H (Hasil), I (Catatan), J (Email).
  - Rumus untuk kolom Status (contoh di sel G7): `=IF(E7=""; ""; IF(E7 < TODAY() - 30; "Expired"; IF(E7<TODAY(); "Dikirim " & (TODAY() - E7) & " hari lalu"; "Hari ini")))`.
- **Sheet "Users"**:
  - Kolom A (Email), B (Password - hashed), C (Name).
- Catat ID Spreadsheet (dari URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).

### 2. Setup Google Apps Script
- Buka Google Apps Script (script.google.com) dan buat proyek baru.
- Hubungkan proyek dengan spreadsheet yang dibuat (gunakan ID di kode).
- Salin kode dari `Code.gs` ke editor script.
- Update konstanta:
  - `SPREADSHEET_ID`: Ganti dengan ID spreadsheet Anda.
  - `ADMIN_EMAIL`: Ganti dengan email admin (misalnya, 'admin@example.com').
- Deploy sebagai web app:
  - Klik "Publish" > "Deploy as web app".
  - Set "Execute as: Me", "Who has access: Anyone".
  - Salin URL web app yang dihasilkan.

### 3. File HTML
- Di proyek GAS, buat file baru bernama "Index.html".
- Salin kode HTML yang disediakan ke file tersebut.
- Pastikan link CDN Bootstrap dan ikon dapat diakses.

### 4. Setup Awal
- Tambahkan setidaknya satu pengguna admin secara manual di sheet "Users" (email, hash password, nama). Gunakan fungsi hashPassword di GAS untuk menghasilkan hash password.
- Test login dengan membuka URL web app.
- Jika perlu, sesuaikan styling atau fungsi di HTML/JS.

### 5. Migrasi ke Lingkungan Lokal (Opsional)
Jika ingin mengembangkan secara lokal:
- Gunakan `clasp` (Command Line Apps Script) untuk push/pull kode.
- Struktur folder: `src/Index.html`, `src/Code.gs`, dll.

## Penggunaan
1. **Login**: Akses URL web app, masukkan email dan password.
2. **Dashboard**: Lihat statistik dan tambahkan lamaran baru via form.
3. **Kelola Lamaran**:
   - Tambah: Isi form dan klik "SIMPAN".
   - Update: Klik ikon edit, pilih status, tambah catatan, simpan.
   - Hapus: Klik ikon hapus dan konfirmasi.
4. **Cari/Filter**: Gunakan search bar atau modal filter.
5. **Admin**: Jika admin, klik ikon shield untuk kelola pengguna.
6. **Pengaturan**: Klik ikon gear untuk ubah password, atau logout.

### Tips Penggunaan
- Lamaran diurutkan berdasarkan tanggal (terbaru dulu).
- Status otomatis dihitung berdasarkan tanggal (mis., "Expired" setelah 30 hari).
- Gunakan mode mobile untuk pengalaman terbaik di ponsel.
- Data disimpan otomatis ke Google Sheets.

## Keamanan
- Password di-hash menggunakan SHA-256 dengan salt unik untuk mencegah brute-force.
- Akses data difilter berdasarkan email pengguna.
- Admin tidak dapat dihapus sendiri.
- Pastikan spreadsheet hanya dibagikan dengan pengguna yang diizinkan.
- Gunakan HTTPS jika memungkinkan, meskipun GAS sudah aman.

## Kontribusi
- Fork repositori ini (jika tersedia di GitHub).
- Buat branch baru untuk fitur atau perbaikan.
- Lakukan perubahan pada file HTML dan Code.gs.
- Test secara menyeluruh di lingkungan pengembangan.
- Buat pull request dengan deskripsi perubahan.

## Lisensi
Proyek ini bersifat proprietary. Hubungi pengembang untuk izin penggunaan atau modifikasi.

## Kontak
Untuk pertanyaan atau dukungan, hubungi pengembang: Pandu Yogatama (atau email terkait).

---
*Dokumentasi ini dibuat dalam mode Technical Writer untuk kejelasan dan struktur yang baik.*
