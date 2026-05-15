# <a name="getting-started"></a>Memulai dengan Spck CLI

## <a name="overview"></a>Gambaran Umum

Spck CLI adalah alat baris perintah yang menghubungkan lingkungan pengembangan lokal Anda ke aplikasi mobile Spck Editor melalui koneksi WebSocket yang aman. Setelah berjalan, Anda dapat menjelajahi dan mengedit file lokal, menjalankan perintah terminal, dan mempratinjau server lokal — semuanya dari ponsel atau tablet Anda.

## <a name="requirements"></a>Persyaratan

### Wajib

- **Node.js**: 18.0.0 atau lebih tinggi
- **Akun Spck Editor**: Akun gratis (30 menit/hari) atau langganan Premium (tanpa batas)
- **Aplikasi Mobile Spck Editor**: [Android](https://play.google.com/store/apps/details?id=io.spck) atau [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### Opsional (Direkomendasikan)

- **Git**: 2.20.0+ untuk fitur integrasi Git
- **ripgrep**: 15.0.0+ untuk pencarian file yang jauh lebih cepat (peningkatan 100x)

## <a name="installation"></a>Instalasi

### Opsi 1: Jalankan dengan npx (Tanpa Instalasi)

```bash
npx spck
```

Selalu menggunakan versi terbaru — sempurna untuk pengaturan pertama kali atau penggunaan sesekali.

### Opsi 2: Instalasi Global

```bash
npm install -g spck
spck
```

Startup lebih cepat, bekerja offline, dan nyaman untuk penggunaan sehari-hari.

## <a name="demo"></a>Demo

Panduan singkat menghubungkan Spck CLI ke aplikasi seluler dan mengedit berkas lokal dari jarak jauh:

<img src="https://docs.spck.io/assets/gifs/remote-cli-preview.gif" alt="Demo Spck CLI" width="100%" />

## <a name="first-time-setup"></a>Pengaturan Pertama Kali

Saat pertama kali menjalankan CLI, wizard pengaturan interaktif akan memandu Anda melalui:

### 1. Autentikasi

```bash
spck
# Tekan ENTER untuk membuka browser
# Masuk dengan akun Spck Editor Anda
# Otorisasi CLI
# Kembali ke terminal
```

Kredensial disimpan di `~/.spck-editor/.credentials.json` dan bertahan antar sesi.

### 2. Konfigurasi Proyek

Wizard akan mengonfigurasi:

- **Direktori root**: Direktori dasar untuk akses file (default: direktori saat ini)
- **Nama proyek**: Nama tampilan di aplikasi mobile (default: nama direktori)

### 3. Integrasi Git (Opsional)

Jika file `.gitignore` terdeteksi, CLI menawarkan untuk menambahkan `.spck-editor/` guna mencegah commit rahasia secara tidak sengaja:

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**Rekomendasi**: Pilih `Y` untuk melindungi kredensial koneksi.

### Jalankan Ulang Pengaturan

Untuk mengonfigurasi ulang kapan saja:

```bash
spck --setup
```

## <a name="connecting"></a>Menghubungkan ke Spck Editor

Setelah CLI berjalan, ia menampilkan kode QR dan detail koneksi.

### Metode 1: Kode QR (Direkomendasikan)

**PENTING**: Instal aplikasi Spck Editor SEBELUM memindai kode QR.

**Di Android:**

1. Gunakan aplikasi Kamera atau pemindai QR di Pengaturan Cepat
2. Saat terdeteksi, ketuk notifikasi untuk membuka Spck Editor
3. Aplikasi terhubung secara otomatis

> 💡 **Catatan**: Beberapa pemindai kode QR tidak dapat menangani skema khusus untuk membuka Spck Editor secara langsung. Salin URL dan tempelkan di Chrome, yang akan meluncurkan Spck Editor dari URL tersebut.

**Di iOS:**

1. Gunakan aplikasi Kamera atau pemindai QR di Pusat Kontrol
2. Saat terdeteksi, ketuk notifikasi untuk membuka Spck Editor
3. Aplikasi terhubung secara otomatis

> 💡 **Catatan**: Spck Editor TIDAK memiliki pemindai QR bawaan. Gunakan kemampuan QR bawaan perangkat Anda.

### Metode 2: Entri Manual

Jika kode QR tidak berfungsi:

1. Buka Spck Editor → **Proyek** → **Proyek Baru** → **Tautkan Server Jarak Jauh**
2. Masukkan **ID Klien** dan **Rahasia** yang ditampilkan di terminal
3. Ketuk **Hubungkan**

## <a name="next-steps"></a>Langkah Selanjutnya

1. **Pahami sistem relay**: Pelajari cara CLI merutekan lalu lintas dan cara memilih server — lihat [Referensi CLI](./cli)
2. **Konfigurasikan pengaturan Anda**: Sesuaikan pengaturan terminal, keamanan, dan sistem file — lihat [Konfigurasi](./cli-config)
3. **Jelajahi fitur lanjutan**: Perintah CLI, agen pengkodean AI, beberapa proyek — lihat [Penggunaan Lanjutan](./cli-advanced)
4. **Transfer file antar perangkat**: Salin proyek antara ponsel dan desktop secara nirkabel — lihat [Transfer File](./cli-file-transfer)
5. **Jaga sesi tetap aktif**: Bagikan sesi antar perangkat dengan tmux — lihat [Menggunakan Tmux](./tmux)
