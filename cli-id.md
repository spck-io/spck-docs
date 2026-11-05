# <a name="cli-reference"></a>Referensi CLI

## <a name="key-features"></a>Fitur Utama

- **Filesystem Jarak Jauh**: Akses dan edit file lokal dari aplikasi mobile Spck Editor
- **Integrasi Git**: Operasi git lengkap (commit, push, pull, manajemen branch) — memerlukan Git 2.20.0+
- **Akses Terminal**: Sesi terminal interaktif dengan xterm.js
- **Browser Proxy**: Pratinjau server lokal Anda dalam tampilan browser layar penuh di dalam Spck Editor
- **Pencarian Cepat**: Pencarian file yang dioptimalkan dengan deteksi ripgrep otomatis (100x lebih cepat saat terinstal)
- **Agen AI Coding Lokal (ACP)**: Jalankan Claude Code, Codex, atau Gemini CLI dari AI Chat Spck Editor melalui [Agent Client Protocol](https://agentclientprotocol.com/). Agen berjalan di mesin Anda dengan langganan Anda sendiri. Lihat [Agen AI Coding di Mobile (ACP)](./cli-acp).
- **Fast Lane** (Supporter & Gold): Koneksi WebRTC peer-to-peer langsung antara Spck Editor dan CLI, rata-rata 2x lebih cepat daripada relay. Lihat [Fast Lane](#fast-lane).
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

## <a name="fast-lane"></a>Fast Lane

Fast Lane adalah fitur premium untuk pelanggan **Supporter** dan **Gold**. Alih-alih mengirim setiap pesan melalui server relay, Spck Editor terhubung **langsung ke CLI Anda** menggunakan WebRTC (peer-to-peer). Dengan menghilangkan perantara relay dan mengurangi bolak-balik data, Fast Lane **rata-rata 2x lebih cepat daripada relay**, sehingga operasi file, pencarian, Git, dan input terminal terasa jauh lebih responsif.

Server relay tetap diperlukan: di sanalah CLI Anda terdaftar, dan relay menengahi handshake awal antara editor dan CLI. Setelah jalur langsung terbentuk, data proyek Anda mengalir melaluinya, bukan melalui relay.

### Persyaratan

- Langganan **Supporter** atau **Gold** yang aktif pada akun yang digunakan untuk masuk di CLI
- Spck CLI **0.7.0 atau lebih baru** (`npm i -g spck`)
- Dukungan WebRTC, baik di perangkat yang menjalankan Spck Editor maupun di mesin yang menjalankan CLI

### Mengaktifkan atau Menonaktifkan Fast Lane

**Di Spck Editor:** Buka **Link Remote Server** (atau edit koneksi yang sudah ada dari menu) lalu gunakan sakelar **⚡ Fast Lane**. Sakelar ini aktif secara default untuk koneksi baru pada akun Supporter dan Gold.

**Di CLI:** Fast Lane aktif secara default. Tekan **`f`** di dasbor CLI untuk mengaktifkan atau menonaktifkannya pada proyek saat ini, atau atur `fastLane.enabled` di [konfigurasi proyek](./cli-config#fast-lane-settings). Perubahan berlaku setelah CLI dimulai ulang. Nonaktifkan di jaringan yang memblokir lalu lintas peer-to-peer.

Dasbor CLI menampilkan status Fast Lane saat ini (aktif, tersedia, dinonaktifkan, atau tidak tersedia di platform ini), dan panel File di Spck Editor menampilkan transport yang sedang digunakan beserta ping saat ini, misalnya `Fast Lane · 24 ms` atau `Relay · 80 ms`.

### Fallback Otomatis

Jika koneksi langsung tidak dapat dibuat, Spck Editor otomatis beralih ke relay agar Anda tetap bisa bekerja, dan menampilkan pemberitahuan yang menjelaskan alasannya. Alasan umum:

- CLI sudah usang — perbarui dengan `npm i -g spck`
- Fast Lane dinonaktifkan di konfigurasi proyek CLI
- WebRTC tidak tersedia di mesin yang menjalankan CLI, atau di perangkat Anda
- Server relay belum mendukung Fast Lane
- Jaringan memblokir jalur peer-to-peer langsung (misalnya firewall perusahaan yang ketat atau NAT)

### Keamanan

Lalu lintas Fast Lane dienkripsi end-to-end oleh WebRTC (DTLS). Selain itu, handshake autentikasi CLI terikat pada sesi DTLS tertentu, sehingga CLI harus membuktikan bahwa ia memegang rahasia koneksi Anda pada kanal yang sama persis sebelum data proyek apa pun dipertukarkan. Semua permintaan tetap ditandatangani secara kriptografis, sama seperti pada relay. Lihat [Keamanan CLI](./cli-config#security).

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
5. Jika muncul pemberitahuan bahwa Fast Lane tidak tersedia dan relay digunakan, koneksi tetap berfungsi melalui relay. Lihat bagian "Fallback Otomatis" di [Fast Lane](#fast-lane) untuk alasan dan solusinya

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

Lite mendukung pengeditan proyek di komputer desktop atau VM publik melalui Spck CLI. Proyek Jarak Jauh memerlukan **akun Spck dan langganan Spck aktif**, terpisah dari pembelian satu kali Lite. Langganan membantu menanggung biaya berkelanjutan untuk hosting, pengoperasian, dan pemeliharaan server Spck. Alat pengeditan lokal dan Git yang disertakan tetap dapat digunakan tanpa langganan.

Jumlah maksimum koneksi CLI simultan dan batas penggunaan harian bergantung pada jenis akun Anda:

| Paket     | Koneksi CLI | Batas Harian | Fast Lane |
| --------- | ----------- | ------------ | --------- |
| Gratis    | 1           | 30 menit     | —         |
| Supporter | 2           | Tidak terbatas | ✓         |
| Gold      | 5           | Tidak terbatas | ✓         |

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
