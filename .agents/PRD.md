# PRD - Sistem Manajemen Peminjaman Mobil Dinas

**Versi:** 1.0
**Tanggal:** 03 September 2026

---

## 📄 BAGIAN 1: Visi & Tujuan Produk

### Visi Produk
Menyediakan sistem digital yang memudahkan staff setiap ruangan dalam mengajukan peminjaman mobil dinas secara transparan, efisien, dan terpantau secara real-time.

### Tujuan Utama
1. **Digitalisasi proses peminjaman** - Mengurangi proses manual dan kertas kerja → Target: 80% permintaan melalui aplikasi dalam 3 bulan
2. **Visibilitas ketersediaan mobil** - Staff bisa lihat status mobil kapan saja → Target: mengurangi konflik peminjaman
3. **Notifikasi real-time** - Admin mendapat notif WhatsApp saat ada permintaan baru → Target: respon < 1 jam
4. **Pelacakan riwayat** - Data peminjaman tercatat untuk laporan → Target: laporan bulanan otomatis

### Value Proposition
- Cek ketersediaan mobil real-time tanpa tanya-tanya
- Approve/Reject langsung dari WhatsApp
- Riwayat peminjaman lengkap per ruangan

---

## 📄 BAGIAN 2: User Persona

### Persona 1: Staff Ruangan (Peminjam)
- **Usia/Pekerjaan:** 25-45 tahun, Staff/Administrasi
- **Level Teknis:** Pemula-Menengah
- **Tujuan:** Ajukan peminjaman mobil dinas untuk keperluan dinas
- **Pain Points:**
  - Harus tanya langsung ke admin untuk cek mobil available
  - Proses lama karena manual
  - Tidak tahu status permintaan sudah diproses atau belum
- **Motivasi:** Mudah, cepat, bisa cek status kapan saja

### Persona 2: Admin/Manager (Pengelola)
- **Usia/Pekerjaan:** 30-50 tahun, Manager/Admin
- **Level Teknis:** Pemula
- **Tujuan:** Kelola permintaan peminjaman, approve/reject, pantau pengembalian
- **Pain Points:**
  - Banyak permintaan lewat chat/WA yang sulit dilacak
  - Sulit cegah bentrok peminjaman
  - Laporan harus dibuat manual
- **Motivasi:** Kontrol penuh, notif langsung, laporan otomatis

---

## 📄 BAGIAN 3: User Stories

### Modul 1: Autentikasi
- Sebagai staff, saya ingin login dengan email/username, agar bisa akses sistem
- Sebagai admin, saya ingin reset password staff, agar bisa bantu jika lupa

### Modul 2: Peminjaman Mobil
- Sebagai staff, saya ingin lihat daftar mobil dan statusnya, agar tahu mana yang available
- Sebagai staff, saya ingin ajukan peminjaman dengan mengisi form, agar permintaan tercatat
- Sebagai staff, saya ingin melihat riwayat peminjaman saya, agar bisa cek status
- Sebagai admin, saya ingin melihat daftar permintaan masuk, agar bisa proses
- Sebagai admin, saya ingin approve/reject permintaan, agar mobil hanya dipinjam yang sah
- Sebagai admin, saya ingin menetapkan plat mobil dan nama driver saat approve, agar jelas penanggung jawab

### Modul 3: Pengembalian
- Sebagai staff, saya ingin konfirmasi pengembalian mobil, agar status mobil kembali available
- Sebagai admin, saya ingin melihat mobil yang belum dikembalikan, agar bisa follow-up

### Modul 4: Laporan
- Sebagai admin, saya ingin export data peminjaman, agar bisa buat laporan bulanan
- Sebagai admin, saya ingin filter data berdasarkan ruangan/tanggal, agar analisis lebih mudah

### Modul 5: Notifikasi
- Sebagai admin, saya ingin mendapat notifikasi WhatsApp saat ada permintaan baru, agar bisa respon cepat
- Sebagai staff, saya ingin mendapat notifikasi saat permintaan di-approve/reject, agar tahu status

---

## 📄 BAGIAN 4: Functional Requirements

### Modul 1: Autentikasi

**FR-01: Login Pengguna**
- **Input:** Username/Email, password
- **Proses:** Verifikasi kredensial, generate session
- **Output:** Akses ke dashboard sesuai role
- **Aturan:** 5x gagal login = blokir 15 menit

**FR-02: Manajemen Akun (Superadmin)**
- **Input:** Data admin baru (nama, email, password)
- **Proses:** CRUD akun admin
- **Output:** Akun admin terdaftar
- **Aturan:** Hanya superadmin yang bisa kelola akun admin

---

### Modul 2: Data Master

**FR-03: Manajemen Ruangan (Superadmin)**
- **Input:** Nama ruangan
- **Proses:** CRUD ruangan
- **Output:** Daftar ruangan
- **Aturan:** Nama ruangan unik

**FR-04: Manajemen Mobil (Superadmin)**
- **Input:** Plat nomor, nama mobil, jenis, tahun, status
- **Proses:** CRUD data mobil
- **Output:** Daftar mobil dengan status
- **Aturan:** Status: Tersedia / Dipinjam / Perawatan

---

### Modul 3: Peminjaman

**FR-05: Form Peminjaman (Staff)**
- **Input:** Tanggal pinjam, rencana tanggal kembali, tempat tujuan, penggunaan, kategori (Operasional/Pbjadi)
- **Proses:** Simpan permintaan dengan status "Menunggu Persetujuan"
- **Output:** Nomor urut peminjaman terbuat, notif ke admin
- **Aturan:** Rencana tanggal kembali harus > tanggal pinjam

**FR-06: Daftar Permintaan (Admin)**
- **Input:** Filter (status, tanggal, ruangan)
- **Proses:** Tampilkan semua permintaan masuk
- **Output:** List permintaan dengan detail
- **Aturan:** Urutkan dari yang terbaru

**FR-07: Approve/Reject Permintaan (Admin)**
- **Input:** ID permintaan, plat mobil, nama driver, status (approve/reject)
- **Proses:** Update status, ubah status mobil jadi "Dipinjam" jika approve
- **Output:** Status berubah, notif WhatsApp ke peminjam
- **Aturan:**
  - Wajib isi plat mobil dan nama driver saat approve
  - Hanya admin yang bisa approve/reject

**FR-08: Riwayat Peminjaman (Staff)**
- **Input:** Filter (tanggal)
- **Proses:** Tampilkan riwayat peminjaman staff yang login
- **Output:** List peminjaman milik staff
- **Aturan:** Staff hanya lihat data sendiri

---

### Modul 4: Pengembalian

**FR-09: Konfirmasi Pengembalian (Staff)**
- **Input:** ID peminjaman
- **Proses:** Update tanggal pengembalian aktual, status mobil kembali "Tersedia"
- **Output:** Status berubah, riwayat tercatat
- **Aturan:** Hanya bisa dikembalikan jika status disetujui

**FR-10: Monitoring Belum Kembali (Admin)**
- **Input:** -
- **Proses:** Cari peminjaman yang melewati rencana tanggal kembali
- **Output:** List mobil overdue
- **Aturan:** Tandai dengan flag "Terlambat"

---

### Modul 5: Laporan

**FR-11: Laporan Peminjaman (Admin/Superadmin)**
- **Input:** Filter (rentang tanggal, ruangan, kategori)
- **Proses:** Agregasi data peminjaman
- **Output:** Tabel dengan kolom: No, Nama Peminjam, Nama Ruangan, Tanggal Order, Tanggal Peminjaman, Rencana Tanggal Pengembalian, Tempat Tujuan, Penggunaan, Kategori, Persetujuan - Plat Mobil, Persetujuan - Nama Driver, Tanggal Pengembalian
- **Aturan:** Bisa export ke Excel/PDF

---

### Modul 6: Notifikasi

**FR-12: Notifikasi WhatsApp ke Admin**
- **Input:** Data permintaan baru
- **Proses:** Kirim WA via API ke nomor admin
- **Output:** Admin terima notif di WA
- **Aturan:** Format: "Permintaan peminjaman dari [Nama] ([Ruangan])"

**FR-13: Notifikasi WhatsApp ke Peminjam**
- **Input:** Status approve/reject
- **Proses:** Kirim WA ke peminjam
- **Output:** Peminjam terima notif status
- **Aturan:** Format: "Permintaan peminjaman anda [Disetujui/Ditolak]"

---

### Modul 7: Manajemen Role

**FR-14: Superadmin**
- **Input:** -
- **Proses:** Kelola semua data (admin, staff, ruangan, mobil)
- **Output:** Full akses sistem
- **Aturan:**
  - Bisa CRUD akun admin
  - Bisa CRUD ruangan
  - Bisa CRUD mobil
  - Bisa akses semua laporan

**FR-15: Admin**
- **Input:** -
- **Proses:** Kelola permintaan peminjaman
- **Output:** Approve/reject, monitoring
- **Aturan:**
  - Bisa approve/reject peminjaman
  - Bisa lihat laporan
  - Tidak bisa kelola akun admin lain

---

## 📄 BAGIAN 5: Non-Functional Requirements

### Performa
- Waktu muat halaman < 2 detik
- API response < 500ms
- Support 100 user concurrent

### Keamanan
- Password di-hash (bcrypt)
- HTTPS wajib
- JWT token expiry 24 jam
- Role-based access control (Superadmin/Admin/Staff)

### Usability
- Responsive (mobile, tablet, desktop)
- Bahasa Indonesia
- Interface sederhana dan intuitif

### Ketersediaan
- Uptime 99%
- Backup data otomatis harian

---

## 📄 BAGIAN 6: Out of Scope & Dependensi

### Out of Scope (V1)
- Integrasi dengan sistem HRIS
- Sistem manajemen driver (profil driver)
- Integrasi dengan sistem pembukuan
- Multi-cabang
- Sistem booking calendaring

### Dependensi
- WhatsApp Business API (untuk notifikasi)
- Database MySQL/PostgreSQL
- Server hosting

### Asumsi
- User punya koneksi internet stabil
- Admin memiliki nomor WhatsApp aktif
- Jumlah mobil dinas < 50 unit
- Struktur role: Superadmin → Admin → Staff

---

## 📊 Tabel Role & Hak Akses

| Role | Akses Utama |
|------|-------------|
| **Superadmin** | Kelola akun admin, kelola ruangan, kelola mobil, akses semua laporan |
| **Admin** | Approve/reject peminjaman, monitoring, lihat laporan |
| **Staff** | Ajukan peminjaman, lihat riwayat sendiri, konfirmasi pengembalian |
