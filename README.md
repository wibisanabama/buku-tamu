# Buku Tamu

Aplikasi web untuk mencatat kunjungan tamu, mengelola pengguna, melihat riwayat kunjungan, dan mengekspor laporan ke Excel.

## Fitur

- Autentikasi pengguna
- Hak akses administrator dan operator
- Pengelolaan data tamu dan foto
- Pengelolaan akun pengguna
- Filter laporan berdasarkan periode
- Ekspor laporan ke format XLSX

## Teknologi

- PHP 8
- MySQL atau MariaDB
- Bootstrap dan SB Admin 2
- jQuery DataTables
- PhpSpreadsheet

## Persyaratan

- PHP 8.1 atau lebih baru
- MySQL atau MariaDB
- Composer
- Web server Apache
- Ekstensi PHP yang dibutuhkan oleh PhpSpreadsheet

## Instalasi

1. Salin project ke direktori web server. Untuk XAMPP, gunakan:

   ```text
   C:\xampp\htdocs\buku-tamu
   ```

2. Instal dependency:

   ```bash
   composer install
   ```

3. Buat database bernama `app_bukutamu`.

4. Buat tabel berikut:

   ```sql
   CREATE TABLE users (
       id_user VARCHAR(5) NOT NULL PRIMARY KEY,
       username VARCHAR(255) NOT NULL,
       password VARCHAR(255) NOT NULL,
       user_role ENUM('admin', 'operator') NOT NULL
   );

   CREATE TABLE buku_tamu (
       id_tamu VARCHAR(5) NOT NULL PRIMARY KEY,
       tanggal DATE NOT NULL,
       nama_tamu VARCHAR(255) NOT NULL,
       alamat TEXT NOT NULL,
       no_hp VARCHAR(13) NOT NULL,
       bertemu VARCHAR(255) NOT NULL,
       kepentingan VARCHAR(255) NOT NULL,
       gambar VARCHAR(255) DEFAULT NULL
   );
   ```

5. Sesuaikan konfigurasi database di `koneksi.php`:

   ```php
   define('HOST_NAME', 'localhost');
   define('USER_NAME', 'root');
   define('PASSWORD', '');
   define('DATABASE_NAME', 'app_bukutamu');
   ```

6. Pastikan Apache dan MySQL berjalan, lalu buka:

   ```text
   http://localhost/buku-tamu/
   ```

## Akun Lokal

| Peran | Username | Password |
|---|---|---|
| Administrator | `admin` | `password` |
| Operator | `operator` | `password` |

Ganti password setelah login apabila aplikasi digunakan di luar lingkungan pengembangan lokal.

## Hak Akses

| Fitur | Administrator | Operator |
|---|---:|---:|
| Dashboard | Ya | Ya |
| Laporan tamu | Ya | Ya |
| Kelola pengguna | Ya | Tidak |
| Kelola buku tamu | Tidak | Ya |

## Struktur Utama

```text
buku-tamu/
|-- assets/                 Aset tampilan dan foto tamu
|-- templates/              Header dan footer halaman
|-- buku-tamu.php           Pengelolaan data tamu
|-- export-laporan.php      Ekspor laporan XLSX
|-- function.php            Fungsi database dan upload
|-- koneksi.php             Konfigurasi database
|-- laporan.php             Riwayat dan filter laporan
|-- login.php               Autentikasi pengguna
|-- users.php               Pengelolaan pengguna
|-- composer.json           Dependency PHP
`-- README.md               Dokumentasi project
```

## Batasan

- Aplikasi ditujukan untuk lingkungan lokal atau internal.
- Konfigurasi database masih disimpan langsung di source code.
- Database awal dan akun pengguna belum disediakan melalui migration atau seeder.
