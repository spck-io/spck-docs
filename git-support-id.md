# <a name="git-support"></a>Dukungan Git

Spck mendukung Git untuk proyek lokal di Android dan iOS, di peramban, serta proyek jarak jauh melalui Spck CLI. Panduan ini membahas kredensial penyedia, pull request, pemeriksaan commit, penyelesaian konflik, dan keterbatasan platform.

Integrasi Git dasar, riwayat commit, dan penyelesaian konflik tersedia dalam versi gratis. [Integrasi Git Lanjutan](#enhanced-git-integration) menambahkan pengelolaan pull request dan diff berkas commit.

## <a name="git-credentials"></a>Kredensial Git dan pull request

Buka **Git menu → Git Credentials**, pilih penyedia, lalu simpan token aksesnya. Tautan pengaturan dan bantuan di bawah terbuka di tab baru agar Anda dapat kembali ke Spck dan menempelkan token.

| Penyedia | Pengaturan token | Izin untuk Git dan pull request |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">Buat token GitHub</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">Panduan pengaturan</a> | Pilih repositori. Tautan memilih **Contents: Read and write**, **Pull requests: Read and write**, dan **Metadata: Read** secara otomatis. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">Buat token GitLab</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">Panduan pengaturan</a> | Tautan memilih cakupan `api` untuk merge request. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">Buat token API</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">Panduan pengaturan</a> | Pilih **Create API token with scopes**, pilih **Bitbucket**, lalu tandai manual `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket`, dan `write:pullrequest:bitbucket`. Autentikasi API memakai email akun Atlassian. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">Panduan membuat PAT</a> | Buka **User settings → Personal access tokens → New Token** di organisasi Anda, pilih organisasi, lalu tandai **Code (Read & write)** secara manual. |

Untuk membuat pull request, lakukan commit dan push cabang sumber, lalu buka **Git menu → Create PR**. Pilih remote dan kredensial, tentukan cabang tujuan yang berbeda, lalu isi judul dan deskripsi. **Generate with AI** dapat menyusun pesan dari perubahan yang di-commit sejak leluhur bersama kedua cabang; lakukan fetch cabang tujuan terlebih dahulu. Tinjau draf sebelum memilih **Create PR**. GitLab membuat merge request.

Pembuatan dan pengelolaan pull request adalah **fitur Premium** dalam [Integrasi Git Lanjutan](#enhanced-git-integration). Lite menyertakannya dalam pembelian aplikasi sekali bayar. Pada aplikasi lengkap, masuk dengan langganan Supporter, Gold, atau Node aktif, atau akun pemilik pembelian terminal Spck for NodeJS seumur hidup.

## <a name="pull-request-management"></a>Pengelolaan pull request (Premium)

Kelola pull request tanpa meninggalkan editor. Remote yang didukung adalah **GitHub.com, GitLab.com, Bitbucket Cloud, dan Azure DevOps**; GitLab menyebutnya merge request.

1. Buka proyek Git dan tambahkan token penyedia di **Git menu → Git Credentials** dengan izin di atas.
2. Buka **Branches menu → Pull Requests**, lalu pilih remote dan kredensial untuk menampilkan permintaan terbuka.
3. Pilih permintaan untuk melihat judul, deskripsi, penulis, cabang sumber dan tujuan, serta status.
4. Pilih berkas yang berubah untuk memeriksa diff hanya baca sebelum menggabungkan.
5. Gunakan **Merge** untuk menggabungkan permintaan yang memenuhi syarat atau **Close** untuk menutup tanpa menggabungkan. Peninjauan, pemeriksaan, izin token, dan aturan cabang tetap berlaku; draf serta permintaan berkonflik tidak dapat digabungkan dari dialog ini.

Gunakan **Refresh** untuk memuat ulang daftar setelah perubahan di penyedia. Detail permintaan juga menautkan ke penyedia untuk peninjauan, pemeriksaan, dan tindakan lainnya.

Mulai permintaan dengan **Git menu → Create PR** seperti di atas. Jika cabang sumber perlu di-push, dialog menawarkan **Push** sebelum pembuatan. Draf AI opsional menggunakan layanan AI yang dikonfigurasi beserta batas penggunaannya; hal ini terpisah dari akses pull request yang disertakan dalam Lite.

Jika pembuatan gagal karena izin token, gunakan tautan penyedia untuk membuat atau memperbarui token, simpan di **Git Credentials**, lalu coba lagi. Draf PR Anda tetap tersimpan.

## <a name="enhanced-git-integration"></a>Integrasi Git Lanjutan

Integrasi Git Lanjutan menambahkan dua alat untuk meninjau dan membagikan perubahan:

- **Pengelolaan pull request:** membuat permintaan, menelusuri permintaan terbuka, memeriksa berkas dan diff, serta menggabungkan atau menutup permintaan. Lihat [Pengelolaan pull request](#pull-request-management) untuk pengaturan dan langkahnya.
- **Pemeriksaan commit:** menelusuri berkas yang berubah dalam commit dan diff-nya tanpa mengubah berkas kerja.

Buka tab **History** di panel Git dan pilih commit untuk melihat berkas yang ditambahkan, diubah, dan dihapus. Pilih berkas untuk membuka diff hanya baca terhadap induk pertama commit. Pada commit pertama, perbandingan menggunakan pohon kosong. Penampil memakai versi yang telah di-commit; perubahan yang belum di-commit tidak memengaruhi diff. Berkas biner tidak dapat ditampilkan sebagai diff teks.

Anda juga dapat menekan lama entri riwayat, atau mengklik kanan, lalu memilih **View Commit**.

Integrasi Git Lanjutan disertakan dengan:

- **Spck Editor Lite:** terbuka permanen lewat pembelian sekali bayar, tanpa perlu masuk.
- **Pembelian terminal Spck for NodeJS seumur hidup:** terbuka permanen untuk akun pemilik; harus masuk.
- **Langganan Supporter, Gold, atau Node:** terbuka selama langganan aktif; harus masuk.

Integrasi Git dasar dan penelusuran riwayat tetap tersedia dalam versi gratis. Lihat [harga](https://spck.io/pricing) untuk detail paket.

## <a name="merge-conflict-resolution"></a>Menyelesaikan konflik penggabungan

Penampil diff juga membantu menyelesaikan konflik di berkas kerja. Fitur ini bagian dari integrasi Git dasar dan tidak memerlukan Premium.

1. Buka berkas berkonflik dari daftar perubahan Git.
2. Untuk setiap konflik, pilih **Accept Current**, **Accept Incoming**, atau **Accept Both**. Anda juga dapat menyunting berkas untuk menggabungkan perubahan secara manual.
3. Tinjau hasilnya. Setelah semua penanda konflik dihapus, pilih **Resolve** di penampil untuk memasukkan berkas yang diselesaikan ke staging.
4. Selesaikan berkas lainnya, lalu commit penggabungan.

Pada perangkat sentuh, tekan lama berkas atau entri Git untuk membuka menu konteks. Huruf status Git melengkapi warna nama berkas agar perubahan lebih mudah dikenali.

## <a name="git-limitations"></a>Keterbatasan Git

### <a name="git-limitations-overview"></a>Ikhtisar

Implementasi Git bergantung pada lokasi penyimpanan proyek dan versi Spck yang digunakan:

| Lingkungan | Implementasi Git | Batasan utama |
| --- | --- | --- |
| Aplikasi Android dan iOS, termasuk Lite serta Spck for NodeJS | **libgit2** yang dikompilasi secara native untuk proyek lokal | Memerlukan proyek di penyimpanan perangkat; sumber daya dan batasan sistem berkas perangkat tetap berlaku. |
| Peramban dan editor sematan | [isomorphic-git](https://isomorphic-git.org/) dalam JavaScript | Batas memori, penyimpanan, dan jaringan peramban. |
| Proyek jarak jauh melalui Spck CLI | **Biner Git** komputer host | Menggunakan sumber daya, sistem berkas, kredensial, dan Git yang terpasang di host. |

Versi seluler saat ini memakai Git native, bukan mesin Git peramban. Jika muncul **Native Git requires a device folder**, pindahkan proyek ke penyimpanan perangkat. Proyek yang hanya tersimpan di basis data peramban editor tidak dapat menggunakan klien Git native seluler.

Pengelolaan pull request memanggil API penyedia langsung dengan token yang disimpan di **Git Credentials**. Cookie login peramban tidak digunakan dan respons API tidak disimpan dalam cache, sehingga penyegaran mengambil status permintaan dan cabang terbaru. Lihat [Kredensial Git dan pull request](#git-credentials) untuk izin serta [Pengelolaan pull request](#pull-request-management) untuk penyedia dan tindakan yang didukung.

### <a name="git-limitations-memory"></a>Batasan memori

- Git native Android dan iOS menjalankan operasi di luar mesin Git JavaScript. Batas memori mesin peramban bukan batas tetap Git seluler.
- Git native tetap membutuhkan memori dan ruang disk tersedia. Repositori atau berkas pack besar dapat melampaui sumber daya perangkat sehingga operasi gagal atau aplikasi dihentikan sistem.
- Git peramban tetap dibatasi anggaran memori JavaScript dan penyimpanan peramban. Berkas pack besar dapat membutuhkan banyak memori sehingga kloning atau fetch gagal.

> 💡 **Kiat:** Untuk repositori besar, gunakan klona dangkal jika memungkinkan atau kerjakan bagian repositori yang lebih kecil.

### <a name="git-limitations-symlinks"></a>Kompatibilitas symlink

- Penyimpanan peramban dan lapisan sistem berkas perangkat editor menggunakan **symlink emulasi** untuk repositori yang berisi tautan simbolis.
- Beralih ke libgit2 di aplikasi seluler tidak menghilangkan batasan sistem berkas atau menjamin symlink sistem operasi yang sebenarnya.
- Tautan emulasi dapat berperilaku berbeda pada alat build, pengelola paket, atau skrip yang mengharapkan symlink asli dan menyelesaikan target saat dijalankan.
- Untuk proyek yang membutuhkan symlink asli, gunakan proyek jarak jauh pada host dengan dukungan sistem berkas dan izin yang sesuai.

### <a name="git-limitations-cli"></a>Menggunakan CLI sebagai alternatif

Untuk repositori besar atau alur kerja yang memerlukan sistem berkas dan alat Git host, gunakan **proyek jarak jauh melalui Spck CLI**. Operasi Git berjalan dengan **biner Git host** sementara Anda menyunting melalui Spck:

- Operasi memakai memori dan disk host, bukan sumber daya perangkat seluler atau peramban.
- Symlink mengikuti dukungan sistem berkas dan izin sistem operasi host.
- Gunakan alat Git host untuk perintah yang tidak tersedia pada kontrol Git editor.

Lihat [Memulai Spck CLI](./cli-start) untuk menghubungkan host. Proyek jarak jauh memerlukan akun Spck dan mengikuti batas akses paket; lihat [Proyek Jarak Jauh](./editor-lite#remote-projects) untuk syarat langganan Lite. Kloning ke penyimpanan perangkat tetap menggunakan klien Git native aplikasi seluler.

## <a name="git-related-guides"></a>Panduan terkait

- [Dukungan Pembaca Layar (Eksperimental)](./screen-reader-support): navigasi aksesibel, kontrol versi, dan masukan.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): alat Git dalam pembelian sekali bayar.
- [Memulai Spck CLI](./cli-start): hubungkan proyek jarak jauh untuk memakai alat Git host.
