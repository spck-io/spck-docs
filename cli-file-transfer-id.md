# <a name="cli-file-transfer"></a>Transfer File Antara Mobile dan Desktop

## <a name="overview"></a>Gambaran Umum

Saat Anda menjalankan Spck CLI di desktop, ia bertindak sebagai hub sinkronisasi antara sistem file desktop Anda dan proyek lokal yang tersimpan di ponsel Anda. Kedua sisi muncul berdampingan di pengelola file Spck Editor — proyek lokal ponsel Anda di sebelah kiri dan file desktop Anda sebagai server jarak jauh yang terhubung — dan Anda dapat menyalin file atau seluruh folder ke arah mana pun menggunakan perintah salin dan tempel standar.

Tidak diperlukan AirDrop, Bluetooth, kabel USB, atau penyimpanan cloud pihak ketiga. Transfer dienkripsi ujung ke ujung melalui koneksi WebSocket dan tetap berada di Wi-Fi lokal Anda ketika kedua perangkat berada di jaringan yang sama.

## <a name="how-it-works"></a>Cara Kerjanya

CLI mengekspos direktori desktop Anda sebagai proyek server jarak jauh di pengelola file Spck Editor. Proyek lokal yang disimpan di ponsel Anda tersimpan di penyimpanan lokal aplikasi. Spck Editor memperlakukan keduanya sebagai lokasi proyek kelas satu, sehingga operasi file apa pun yang berfungsi dalam satu proyek — termasuk salin dan tempel — juga berfungsi di antara keduanya.

```
Ponsel (penyimpanan lokal)     Desktop (via CLI)
─────────────────────────      ─────────────────────
my-project/               ↔   ~/projects/my-project/
  ├── index.html                 ├── index.html
  ├── style.css                  ├── style.css
  └── assets/                    └── assets/
      └── logo.png                   └── logo.png
```

Direktori ditransfer secara rekursif — semua file di dalamnya disalin, dengan subdirektori dibuat secara otomatis di tujuan.

## <a name="desktop-to-mobile"></a>Desktop ke Mobile

Gunakan ini saat Anda ingin membawa file dari komputer ke ponsel — misalnya, untuk bekerja offline, berbagi proyek dengan rekan yang hanya memiliki aplikasi mobile, atau mengambil snapshot pekerjaan Anda ke perangkat.

1. **Mulai CLI** di desktop Anda, mengarah ke folder yang ingin Anda transfer:

   ```bash
   spck --root ~/projects
   ```

2. **Hubungkan ponsel Anda** dengan memindai kode QR menggunakan aplikasi kamera dan membuka tautan di Spck Editor.

3. Di Spck Editor, folder desktop Anda muncul sebagai proyek server jarak jauh di panel **Proyek**.

4. **Tekan lama file atau folder** yang Anda inginkan di proyek jarak jauh, lalu ketuk **Salin**.

5. **Navigasi ke proyek lokal** di ponsel Anda (atau buat yang baru melalui **Proyek Baru**).

6. **Tekan lama folder tujuan**, lalu ketuk **Tempel**.

File diunduh dari desktop Anda dan disimpan ke penyimpanan lokal ponsel Anda.

## <a name="mobile-to-desktop"></a>Mobile ke Desktop

Gunakan ini saat Anda ingin mengirim pekerjaan dari ponsel kembali ke desktop — misalnya, setelah mengedit saat bepergian, atau untuk mengonsolidasikan proyek yang dibuat di perangkat.

1. **Mulai CLI** di desktop Anda, mengarah ke folder tempat Anda ingin file berada:

   ```bash
   spck --root ~/Desktop/from-phone
   ```

2. **Hubungkan ponsel Anda** dengan memindai kode QR.

3. Di Spck Editor, buka **proyek lokal** di ponsel Anda yang berisi file yang ingin Anda kirim.

4. **Tekan lama file atau folder** yang Anda inginkan, lalu ketuk **Salin**.

5. **Navigasi ke proyek desktop jarak jauh** di panel **Proyek**.

6. **Tekan lama folder tujuan**, lalu ketuk **Tempel**.

File dibaca dari penyimpanan lokal ponsel Anda dan ditulis ke desktop Anda melalui CLI.

## <a name="transferring-projects"></a>Mentransfer Seluruh Proyek

Anda dapat menyalin seluruh folder proyek dalam satu operasi tempel. Tekan lama root proyek di pohon file dan pilih **Salin**, lalu navigasi ke tujuan dan **Tempel**. Seluruh pohon direktori — termasuk semua file di semua subdirektori — ditransfer.

Ini berguna untuk:

- **Mencadangkan proyek mobile ke desktop** sebelum melakukan perubahan besar
- **Menyemai proyek baru di ponsel** dari basis kode desktop yang sudah ada
- **Menggabungkan pekerjaan** dari beberapa perangkat ke satu lokasi

## <a name="tips"></a>Tips

### Batas Ukuran File

Ukuran file maksimum default adalah **10 MB** per file. Untuk mentransfer file yang lebih besar seperti gambar, arsip, atau biner yang dikompilasi, tingkatkan batasnya di konfigurasi CLI Anda:

```json
{
  "filesystem": {
    "maxFileSize": "200MB"
  }
}
```

Lihat [Konfigurasi CLI](./cli-config) untuk detail lengkap.

### Kecepatan Transfer

Kecepatan sepenuhnya bergantung pada koneksi Wi-Fi lokal atau internet Anda. Untuk direktori besar, transfer berjalan file demi file, sehingga throughput keseluruhan skala dengan jumlah file. Di jaringan Wi-Fi rumah tipikal, proyek kecil yang padat teks (ratusan file) selesai dalam beberapa detik.

### Keamanan

Semua transfer dienkripsi melalui WSS (WebSocket Secure) dan setiap permintaan ditandatangani dengan kunci rahasia per sesi. Server relay meneruskan pesan antar perangkat tetapi tidak pernah menerima konten yang tidak dienkripsi. Lihat [Keamanan CLI](./cli-config#security) untuk detail lengkap.

### Menjalankan Beberapa Transfer

CLI mengekspos satu direktori root. Untuk mentransfer dari beberapa lokasi secara bersamaan, jalankan instans CLI terpisah di terminal yang berbeda:

```bash
# Terminal 1: ekspos ~/projects
spck --root ~/projects

# Terminal 2: ekspos ~/Documents
spck --root ~/Documents
```

Setiap instans menghasilkan kode QR dan koneksinya sendiri, dan kedua server jarak jauh muncul di panel **Proyek** Spck Editor secara bersamaan.
