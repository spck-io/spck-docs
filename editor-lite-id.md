# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>Ringkasan

Spck Editor Lite adalah versi pembelian satu kali dari Spck Editor yang membuka fitur pengeditan premium tanpa langganan. Aplikasi ini tersedia sebagai aplikasi terpisah di Android maupun iOS.

Lite mencakup semua yang ada di versi gratis, ditambah:

- **Predictive Keyboard** -- saran simbol kontekstual pada keyboard tambahan
- **Snippet Kustom** -- template kode buatan pengguna dengan placeholder tab stop
- **Tema Neon** -- tema editor eksklusif
- **Integrasi Git Lanjutan** — Pengelolaan pull request ; Perubahan berkas dan diff commit

Fitur-fitur ini juga tersedia di versi lengkap Spck Editor dengan langganan Gold atau Supporter yang aktif. Aplikasi Lite menyediakan fungsionalitas yang sama sebagai pembelian satu kali.

Untuk fokus papan ketik, aktivasi menu, dan penyuntingan aksesibel, lihat [Dukungan Pembaca Layar (Eksperimental)](./screen-reader-support).

## <a name="remote-projects"></a>Proyek Jarak Jauh

Lite mendukung pengeditan proyek di komputer desktop atau VM publik melalui Spck CLI. Proyek Jarak Jauh memerlukan **akun Spck dan langganan Spck aktif**, terpisah dari pembelian satu kali Lite. Langganan membantu menanggung biaya berkelanjutan untuk hosting, pengoperasian, dan pemeliharaan server Spck. Alat pengeditan lokal dan Git yang disertakan tetap dapat digunakan tanpa langganan.

[Spck CLI](./cli-start) · [Spck](https://spck.io/pricing)

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

## <a name="enhanced-git-integration"></a>Integrasi Git Lanjutan

### Pengelolaan pull request (Premium)

Lite menyertakan alat pull request Premium yang sama dengan aplikasi lengkap, tanpa langganan. Lihat [Pengelolaan pull request](./git-support#pull-request-management) untuk membuat dan menelusuri permintaan, meninjau diff, serta menggabungkan atau menutupnya sesuai aturan penyedia.

Simpan token di **Git menu → Git Credentials**. Gunakan **Git menu → Create PR** untuk membuat permintaan dan **Git menu → Pull Requests** untuk mengelolanya. Draf AI opsional memerlukan layanan yang dikonfigurasi dan bukan jatah kredit AI yang disertakan dalam Lite.

### Perubahan berkas dan diff commit

Buka tab **History** di panel Git dan pilih commit untuk melihat berkas yang ditambahkan, diubah, dan dihapus. Pilih berkas untuk membuka diff hanya baca terhadap induk pertama commit. Pada commit pertama, perbandingan menggunakan pohon kosong. Penampil memakai versi yang telah di-commit; perubahan yang belum di-commit tidak memengaruhi diff. Berkas biner tidak dapat ditampilkan sebagai diff teks.

Anda juga dapat menekan lama entri riwayat, atau mengklik kanan, lalu memilih **View Commit**.

Integrasi Git Lanjutan disertakan dengan:

- **Spck Editor Lite:** terbuka permanen lewat pembelian sekali bayar, tanpa perlu masuk.
- **Pembelian terminal Spck for NodeJS seumur hidup:** terbuka permanen untuk akun pemilik; harus masuk.
- **Langganan Supporter, Gold, atau Node:** terbuka selama langganan aktif; harus masuk.

Lihat [Dukungan Git](./git-support) untuk [pengaturan token](./git-support#git-credentials), [pengelolaan pull request](./git-support#pull-request-management), dan [Integrasi Git Lanjutan](./git-support#enhanced-git-integration).

## <a name="comparison"></a>Perbandingan Fitur

| Fitur | Gratis | Lite (Sekali Beli) | Lengkap (Langganan) |
| --- | :---: | :---: | :---: |
| Pengeditan kode dan penyorotan sintaks | Ya | Ya | Ya |
| Integrasi Git | Ya | Ya | Ya |
| Integrasi Git Lanjutan | -- | Ya | Supporter / Gold / Node |
| Keyboard Tambahan | Ya | Ya | Ya |
| Keyboard Sentuh dan Kursor | Ya | Ya | Ya |
| Pratinjau proyek | Ya | Ya | Ya |
| Predictive Keyboard | -- | Ya | Gold / Supporter |
| Snippet Kustom | -- | Ya | Gold |
| Tema Neon | -- | Ya | -- |
| Asisten AI | -- | -- | Ya |
| Sinkronisasi cloud | -- | -- | Ya |
| Labs / Proyek komunitas | -- | -- | Ya |
