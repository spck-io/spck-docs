# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>Gambaran Umum

Spck CLI menyertakan jembatan Language Server Protocol (LSP) lengkap yang menjalankan server bahasa untuk TypeScript, JavaScript, Python, HTML, CSS, dan SCSS langsung di host jarak jauh Anda. Saat terhubung ke sesi CLI, Spck Editor secara otomatis menggunakan server bahasa jarak jauh, bukan server bahasa bawaan di perangkat mobile.

> 💡 **Tips**: Untuk deskripsi server bahasa bawaan yang tersedia tanpa CLI, lihat [Editor Language Server](./editor-language-server).

## <a name="cli-ls-architecture"></a>Arsitektur

Server bahasa CLI berjalan di mesin yang sama dengan file proyek Anda. Ini memiliki beberapa keunggulan signifikan dibandingkan pendekatan berbasis browser yang digunakan di perangkat mobile:

### Tanpa Transmisi File

Dengan server bahasa mobile bawaan, file harus dikirim ke perangkat dan dimuat ke dalam worker browser sebelum server bahasa dapat menganalisisnya. Dengan CLI, server bahasa membaca file langsung dari disk — tanpa transmisi. Hal ini menghilangkan overhead bandwidth dan menjaga analisis tetap cepat bahkan pada proyek yang besar.

### Pemahaman Proyek Penuh

Server bahasa CLI memiliki akses ke seluruh direktori proyek Anda, termasuk:

- Semua file sumber di setiap subdirektori
- `node_modules/` untuk resolusi tipe dari pihak ketiga
- File `tsconfig.json` yang ditemukan otomatis di kedalaman mana pun
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` dan file deklarasi terkait

Artinya, fitur pergi ke definisi, cari referensi, dan ganti nama simbol bekerja dengan benar lintas batas file — bahkan saat Anda belum membuka file tersebut di editor.

### Penanganan `tsconfig.json` yang Tepat

Server bahasa TypeScript secara otomatis menemukan dan menghormati `tsconfig.json` (atau `jsconfig.json`) proyek Anda. Alias jalur (`paths`), opsi compiler (`strict`, `target`, `lib`), referensi proyek, dan tata letak workspace monorepo semuanya ditangani dengan benar. Server bahasa mobile bawaan tidak dapat membaca `tsconfig.json` karena tidak memiliki akses ke sistem file saat startup.

### Proses Persisten

Proses server bahasa tetap berjalan selama sesi CLI Anda berlangsung. Ini membangun indeks dalam memori dari proyek Anda dan mempertahankannya antar pengeditan, sehingga respons tetap cepat bahkan setelah startup awal.

## <a name="cli-ls-features"></a>Fitur yang Didukung

| Fitur | Deskripsi |
| --- | --- |
| **Penyelesaian Kode** | Saran berbasis konteks dengan tanda tangan tipe, diurutkan berdasarkan relevansi |
| **Info Hover** | Informasi tipe dan dokumentasi JSDoc untuk simbol di bawah kursor |
| **Bantuan Tanda Tangan** | Petunjuk parameter dan dokumentasi saat mengetik panggilan fungsi |
| **Pergi ke Definisi** | Lompat ke deklarasi simbol mana pun, termasuk yang ada di `node_modules` |
| **Cari Referensi** | Daftar setiap penggunaan simbol di seluruh proyek |
| **Ganti Nama Simbol** | Mengganti nama simbol dan memperbarui semua referensi secara atomik |
| **Diagnostik** | Sorotan kesalahan dan peringatan secara real-time saat Anda mengetik |
| **Rendering Markdown** | Dokumentasi hover dan tanda tangan dirender sebagai Markdown dengan blok kode berwarna sintaks |

## <a name="cli-ls-languages"></a>Bahasa yang Didukung

| Bahasa | Penyelesaian | Hover | Tanda Tangan | Diagnostik |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>Konfigurasi

Dukungan server bahasa diaktifkan secara default. Anda dapat mengontrolnya di file konfigurasi Anda:

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): Sakelar utama untuk semua server bahasa jarak jauh. Default: `true`.
- **`languageServer.typescript.enabled`** (boolean): Aktifkan server bahasa TypeScript/JavaScript. Default: `true`.
- **`languageServer.python.enabled`** (boolean): Aktifkan server bahasa Python (memerlukan `pylsp` di `PATH`). Default: `true`.

## <a name="cli-ls-requirements"></a>Persyaratan

- **TypeScript / JavaScript**: Disertakan dengan CLI. Tidak diperlukan instalasi tambahan.
- **Python**: Memerlukan [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) (`pip install python-lsp-server`).
- **HTML / CSS / SCSS**: Disertakan dengan CLI. Tidak diperlukan instalasi tambahan.

## <a name="cli-ls-vs-mobile"></a>CLI vs. Server Bahasa Mobile

| Kemampuan | CLI Language Server | Bawaan Mobile |
| --- | --- | --- |
| Akses file proyek penuh | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| Resolusi tipe `node_modules` | ✓ | — |
| Pergi ke definisi lintas file | ✓ | Terbatas |
| Cari referensi lintas file | ✓ | — |
| Ganti nama simbol | ✓ | — |
| Dukungan Python | ✓ | — |
| Berfungsi offline (tanpa CLI) | — | ✓ |

&nbsp;

&nbsp;
