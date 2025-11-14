# SIA (Sistem Informasi Akuntansi)

Dokumentasi ini menjelaskan gambaran sistem, cara setup lokal, dan struktur folder yang kini sudah dirapikan agar siap dipublikasikan ke GitHub.

## Gambaran Sistem
- Aplikasi PHP untuk pencatatan akuntansi: Cashflow, Piutang, Hutang, Aset, Jurnal, dan Kontak.
- Role pengguna: `admin`, `supervisor`, `staff`, `head` dengan kontrol izin modular.
- Jurnal otomatis saat proses approval/transaksi tertentu.
- Fitur ekspor laporan ke CSV/Excel.

## Struktur Folder (Aktual)
- `includes/`
  - `config.php` — konfigurasi MySQL standar + helper (session, permission, formatter).
  - `header.php` — komponen navigasi yang di-include oleh halaman.
- `handlers/`
  - `approve_handler.php`, `edit_handler.php`, `payable_approve_handler.php`,
  - `payable_payment_handler.php`, `payable_return_handler.php`,
  - `receivable_payment_handler.php`, `receivable_return_handler.php`.
  - Berisi endpoint POST yang dipanggil dari form di halaman modul.
- `exports/`
  - `export_assets.php`, `export_cashflow.php`, `export_journal.php`,
  - `export_ledger.php`, `export_payables.php`, `export_receivables.php`, `export_trial_balance.php`.
- `scripts/`
  - Utilitas admin: `setup_admin.php`, `secret_reset_database.php`, `fix_data.php`, `generate_password.php`.
- `sql/`
  - `akuntansi.sql` — dump skema/data awal untuk bootstrap database.
- Root (halaman utama)
  - `index.php`, `login.php`, `logout.php`, `manage_users.php`,
  - `cashflow.php`, `receivables.php`, `receivable_history_page.php`,
  - `payables.php`, `payable_history_page.php`, `assets.php`,
  - `journal.php`, `ledger.php`, `trial_balance.php`,
  - `customers.php`, `suppliers.php`, `accounts.php`, `external.php`, `.htaccess`.

Catatan: semua halaman kini meng-include file menggunakan path berbasis `__DIR__` untuk konsistensi.

## Setup Lokal
Prasyarat:
- PHP 7.4+ (disarankan 8.x) dan MySQL/MariaDB tersedia.

Langkah:
1. Buat database baru (mis. `sia`) lalu import `sql/akuntansi.sql`.
2. Konfigurasi DB di `includes/config.php`. Secara default:
   - Host: `localhost`, Port: `3306`, User: `root`, Password: `''`, DB: `sia`, Charset: `utf8mb4`.
   - Mendukung environment vars: `DB_HOST`, `DB_PORT`, `DB_USER`, `DB_PASS`, `DB_NAME`, `DB_CHARSET`.
3. Jalankan server development dari root project:
   - `php -S localhost:8000`
4. Akses aplikasi di `http://localhost:8000`.
5. (Opsional) Jalankan `scripts/setup_admin.php` untuk membuat/refresh user admin default.

## Keamanan & Operasional
- File `scripts/secret_reset_database.php` sangat sensitif — gunakan hanya di lokal/dev dan ubah `RESET_PASSWORD` terlebih dahulu.
- Pastikan hak akses file/folder aman saat di-deploy ke server produksi.

## Kontribusi & Pengembangan
- Issue dan PR dipersilakan untuk perbaikan bug, penambahan test, atau peningkatan arsitektur.
- Rencana berikutnya: memisahkan asset statis ke folder `assets/` dan menambah test dasar untuk modul inti.

---
Selesai. Struktur sudah disederhanakan dan konsisten untuk maintenance jangka panjang.
