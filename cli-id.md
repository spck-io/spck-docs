# <a name="cli-reference"></a>Referensi CLI

## <a name="key-features"></a>Fitur Utama

- **Filesystem Jarak Jauh**: Akses dan edit file lokal dari aplikasi mobile Spck Editor
- **Integrasi Git**: Operasi git lengkap (commit, push, pull, manajemen branch) — memerlukan Git 2.20.0+
- **Akses Terminal**: Sesi terminal interaktif dengan xterm.js
- **Browser Proxy**: Pratinjau server lokal Anda dalam tampilan browser layar penuh di dalam Spck Editor
- **Pencarian Cepat**: Pencarian file yang dioptimalkan dengan deteksi ripgrep otomatis (100x lebih cepat saat terinstal)
- **Aman**: Permintaan yang ditandatangani secara kriptografis dengan autentikasi Firebase opsional

## <a name="relay-server"></a>Server Relay

CLI terhubung ke Spck Editor melalui server relay yang meneruskan pesan di antara keduanya. Pada pertama kali dijalankan, CLI secara otomatis memilih server relay dengan latensi terendah dan menyimpan preferensi ke `~/.spck-editor/.credentials.json`.

**PENTING**: Baik CLI maupun klien Spck Editor harus menggunakan server relay yang sama untuk terhubung. Jika klien tidak dapat menemukan CLI, verifikasi bahwa kedua sisi telah memilih server relay yang sama.

### Server Relay yang Tersedia

| Wilayah       | URL                 |
| ------------- | ------------------- |
| Eropa         | `cli-eu-1.spck.io`  |
| Amerika Utara | `cli-na-1.spck.io`  |
| Asia Selatan  | `cli-sas-1.spck.io` |
| Asia Timur    | `cli-ea-1.spck.io`  |

### Mengganti Server Relay

```bash
# Use a specific relay server
spck --server cli-eu-1.spck.io

# Short form
spck -s cli-na-1.spck.io
```

Penggantian disimpan dan digunakan kembali pada jalankan berikutnya. Untuk menjalankan ulang pemilihan otomatis, hapus kredensial Anda dan mulai ulang:

```bash
spck --logout
spck
```

### Memilih Server Relay di Spck Editor

Saat menghubungkan dari aplikasi mobile melalui **Link Remote Server**, pilih server relay yang sama dari dropdown **Relay Server** yang digunakan oleh CLI. Nama server relay ditampilkan di output CLI setelah terhubung.

## <a name="daily-workflow"></a>Alur Kerja Harian

### Memulai Sesi Anda

```bash
cd /path/to/project
spck
# Connect from mobile app (auto-connects to saved server)
# Start coding
```

### Mengedit File

1. Jelajahi file di aplikasi mobile
2. Ketuk untuk membuka dan mengedit
3. File tersimpan secara otomatis ke komputer Anda

### Menjalankan Perintah Git

**Opsi 1 - GUI Aplikasi Mobile:**

- Buka panel Git
- Lihat perubahan, stage file
- Commit dan push

**Opsi 2 - Terminal:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### Sesi Terminal

Ketuk ikon terminal di aplikasi mobile untuk akses shell penuh dengan izin pengguna Anda.

### Mengakhiri Sesi Anda

```bash
# Keep CLI running for quick reconnects (recommended)
# Or stop with Ctrl+C
```

## <a name="troubleshooting"></a>Pemecahan Masalah

### Direktori Root Tidak Ditemukan

```bash
# Reconfigure with correct path
spck --setup

# Or specify directly
spck --root /correct/path/to/project
```

### Konfigurasi Rusak

```bash
# Clear settings and start fresh
spck --logout
spck --setup
```

### Masalah Koneksi

1. Periksa koneksi internet
2. Verifikasi bahwa CLI dan Spck Editor keduanya menggunakan **server relay yang sama** (ditampilkan di output CLI setelah terhubung)
3. Coba logout dan hubungkan kembali:
   ```bash
   spck --logout
   spck
   ```
4. Periksa pengaturan firewall — pastikan koneksi WebSocket (port 443) diizinkan

### Kode QR Tidak Dapat Dipindai

- Verifikasi aplikasi Spck Editor sudah terinstal sebelum memindai
- Gunakan entri manual: Projects → New Project → Link Remote Server
- Gunakan aplikasi Kamera native, bukan pemindai pihak ketiga

### Operasi Git Tidak Berfungsi

1. Verifikasi Git sudah terinstal:

   ```bash
   git --version  # Requires 2.20.0+
   ```

2. Instal jika diperlukan:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Download from git-scm.com
   ```

### Performa Pencarian Lambat

Instal ripgrep untuk pencarian 100x lebih cepat:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI automatically detects and uses ripgrep
```

### Izin Ditolak

```bash
# View permissions
ls -la /path/to/file

# Fix if needed
chmod 644 /path/to/file

# Don't use sudo - CLI should run as the user who owns the files
```

## <a name="connection-limits"></a>Batas Koneksi

Jumlah maksimum koneksi CLI simultan dan batas penggunaan harian bergantung pada jenis akun Anda:

| Paket     | Koneksi CLI | Batas Harian |
| --------- | ----------- | ------------ |
| Gratis    | 1           | 30 menit     |
| Supporter | 2           | Tidak terbatas |
| Gold      | 5           | Tidak terbatas |

Penggunaan tingkat gratis direset setiap hari pada pukul 12:00 AM UTC.

Ketika batas koneksi tercapai:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

Ketika batas tingkat gratis harian tercapai:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

Periksa koneksi aktif:

```bash
spck --account
```

> 💡 **Catatan**: Hanya satu perangkat mobile yang dapat terhubung ke instans CLI pada satu waktu. Setiap instans CLI menggunakan satu slot koneksi.

## <a name="support"></a>Dukungan

- **Situs Web**: [https://spck.io](https://spck.io)
- **Dukungan**: Hubungi melalui aplikasi mobile Spck Editor
