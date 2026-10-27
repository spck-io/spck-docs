# <a name="screen-reader-support"></a>Dukungan Pembaca Layar (Eksperimental)

Dukungan pembaca layar bersifat **eksperimental** dan mencakup alur kerja utama editor. Kompatibilitas dapat berbeda menurut perangkat, sistem operasi, dan pembaca layar; beberapa kontrol serta fitur penyuntingan lanjutan mungkin masih perlu diperbaiki.

## <a name="screen-reader-activation"></a>Mengaktifkan penyuntingan dengan pembaca layar

Aktifkan pembaca layar di pengaturan aksesibilitas perangkat. Pada versi seluler yang melaporkan status pembaca layar, Spck otomatis menampilkan dokumen aktif sebagai bidang teks yang aksesibel. Tidak ada pengaturan editor terpisah untuk mengaktifkan mode ini.

Bidang teks menyediakan isi dokumen dan nama berkas untuk dibaca, dipilih, dan disunting. Perubahan menggunakan penyimpanan otomatis biasa; pilihan teks tetap sinkron, dan urungkan serta ulangi tetap tersedia. Berpindah berkas memperbarui isi dan namanya; dokumen hanya baca tetap hanya baca. Menonaktifkan pembaca layar mengembalikan editor biasa pada versi yang mendukungnya.

## <a name="screen-reader-navigation"></a>Navigasi dan kontrol

Alur kerja yang didukung meliputi:

- Label dalam bahasa antarmuka untuk tombol ikon, tab navigasi dan berkas, kontrol pencarian, serta tindakan kontrol versi.
- Baris berkas dan proyek yang dapat diaktifkan dengan pembaca layar atau papan ketik. Folder melaporkan status terbukanya; gunakan panah kanan dan kiri pada papan ketik fisik untuk membuka dan menutup folder.
- Tab yang menunjukkan berkas aktif dan huruf status Git yang melengkapi warna nama berkas.
- Pengaturan dengan label dan status terkait serta bidang formulir yang menyediakan informasi kesalahan validasi.
- Dialog bernama yang mempertahankan fokus papan ketik di dalam saat terbuka dan mengembalikannya ke kontrol pemicu saat ditutup. Menu tindakan memindahkan fokus ke isinya dan mengembalikannya saat ditutup dengan Escape.

Pada papan ketik fisik, gunakan **Tab** untuk berpindah kontrol, **Enter** atau **Spasi** untuk mengaktifkan tombol, dan **Escape** untuk menutup menu tindakan. Anda juga dapat menggunakan gestur navigasi dan aktivasi pembaca layar seperti biasa.

## <a name="screen-reader-limitations"></a>Keterbatasan saat ini

- Penyuntingan aksesibel bergantung pada aplikasi seluler yang melaporkan bahwa pembaca layar aktif. Peramban dan editor sematan tidak mengaktifkan mode ini secara otomatis.
- Dukungan saat ini mencakup alur kerja utama di atas. Interaksi editor lanjutan dan fitur lain mungkin tidak bekerja sama baiknya dengan setiap pembaca layar.
- Perilaku dapat berbeda menurut versi aplikasi, sistem operasi, dan perangkat. Laporkan kontrol yang tidak dapat dijangkau atau diaktifkan, perubahan fokus tak terduga, serta masalah membaca atau menyunting.

Lihat [Pintasan Papan Ketik](./editor#keyboard-shortcuts) untuk perintah penyuntingan dan [Dukungan serta Keterbatasan Git](./git-support#git-limitations) untuk perbedaan Git seluler, peramban, dan jarak jauh.

## <a name="screen-reader-feedback"></a>Masukan

[Kirim masukan ke support@spck.io](mailto:support@spck.io) jika kontrol tidak bernama, fokus hilang, atau pembacaan maupun penyuntingan tidak bekerja sesuai harapan. Sertakan versi Spck, perangkat dan sistem operasi, nama pembaca layar, serta langkah untuk mereproduksi masalah.
