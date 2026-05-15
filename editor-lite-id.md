# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Ringkasan

Spck Editor Lite adalah versi pembelian satu kali dari Spck Editor yang membuka fitur pengeditan premium tanpa langganan. Aplikasi ini tersedia sebagai aplikasi terpisah di Android maupun iOS.

Lite mencakup semua yang ada di versi gratis, ditambah:

- **Predictive Keyboard** -- saran simbol kontekstual pada keyboard tambahan
- **Snippet Kustom** -- template kode buatan pengguna dengan placeholder tab stop
- **Tema Neon** -- tema editor eksklusif

Fitur-fitur ini juga tersedia di versi lengkap Spck Editor dengan langganan Gold atau Supporter yang aktif. Aplikasi Lite menyediakan fungsionalitas yang sama sebagai pembelian satu kali.

## <a name="predictive-keyboard"></a>Predictive Keyboard

Predictive Keyboard menggantikan Keyboard Tambahan standar dengan baris tombol simbol kontekstual. Alih-alih menekan lama tombol untuk memilih dari menu, simbol yang paling mungkin ditampilkan langsung berdasarkan posisi kursor dalam file.

### Cara Kerja

Prediksi dihasilkan dari tabel frekuensi statistik yang dibuat per bahasa. Saat kursor berpindah, keyboard mengurutkan ulang simbol berdasarkan seberapa sering masing-masing muncul pada jenis posisi tersebut dalam kode nyata. Bahasa yang didukung meliputi JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown, dan teks biasa.

### Mengaktifkan atau Menonaktifkan

Buka `Settings > Touch > Predictive Keyboard` untuk mengaktifkan atau menonaktifkan fitur ini. Di Lite, Predictive Keyboard diaktifkan secara default. Menonaktifkannya akan mengembalikan Keyboard Tambahan standar.

> Predictive Keyboard hanya tersedia pada perangkat layar sentuh. Fitur ini tidak muncul saat menggunakan keyboard fisik atau dalam mode tablet dengan keyboard eksternal yang terhubung.

## <a name="custom-snippets"></a>Snippet Kustom

Snippet Kustom memungkinkan Anda membuat template kode yang dapat digunakan kembali dan muncul di daftar pelengkapan otomatis saat Anda mengetik. Setiap snippet dikaitkan dengan bahasa tertentu sehingga snippet JavaScript Anda tidak mengacaukan file Python.

### Membuat Snippet

1. Buka `Settings > Editor > Custom Snippets`
2. Pilih bahasa (misalnya JavaScript, Python, HTML)
3. Ketuk **Tambah Snippet**
4. Masukkan **pemicu** -- singkatan yang Anda ketik untuk memanggil snippet
5. Masukkan **isi** -- kode yang akan disisipkan

### Tab Stop dan Placeholder

Snippet mendukung tab stop sehingga kursor melompat di antara posisi yang dapat diedit setelah penyisipan:

- `$1`, `$2`, `$3` -- tab stop bernomor sesuai urutan traversal
- `$0` -- posisi kursor akhir setelah semua tab stop
- `${1:defaultText}` -- tab stop dengan teks placeholder yang dipilih sebelumnya untuk penggantian mudah

Contoh -- snippet loop `for` JavaScript:

**Pemicu:** `forloop`

**Isi:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

Mengetik `forloop` dan memilihnya dari pelengkapan otomatis akan menyisipkan loop lengkap. Tekan Tab untuk berpindah antara `i`, `array`, dan isi loop.

### Impor dan Ekspor

Anda dapat mengekspor semua snippet ke file dan mengimpornya di perangkat lain. Ini berguna untuk berbagi koleksi snippet antar ponsel atau mencadangkan konfigurasi Anda.

## <a name="neon-theme"></a>Tema Neon

Lite menyertakan tema editor **Neon**, tema gelap dengan warna aksen yang cerah. Tema ini ditetapkan sebagai tema default di Lite dan dapat diubah kapan saja di `Settings > Appearance > Theme`.

## <a name="comparison"></a>Perbandingan Fitur

| Fitur | Gratis | Lite (Sekali Beli) | Lengkap (Langganan) |
| --- | :---: | :---: | :---: |
| Pengeditan kode dan penyorotan sintaks | Ya | Ya | Ya |
| Integrasi Git | Ya | Ya | Ya |
| Keyboard Tambahan | Ya | Ya | Ya |
| Keyboard Sentuh dan Kursor | Ya | Ya | Ya |
| Pratinjau proyek | Ya | Ya | Ya |
| Predictive Keyboard | -- | Ya | Gold / Supporter |
| Snippet Kustom | -- | Ya | Gold / Supporter |
| Tema Neon | -- | Ya | -- |
| Asisten AI | -- | -- | Ya |
| Akun pengguna dan sinkronisasi cloud | -- | -- | Ya |
| Labs / Proyek komunitas | -- | -- | Ya |
