# <a name="cli-configuration"></a>Konfigurasi CLI

## <a name="configuration"></a>Konfigurasi

### Lokasi File Konfigurasi

Konfigurasi disimpan di `.spck-editor/config/spck-cli.config.json` di direktori proyek Anda.

**Penting**: `.spck-editor/config` adalah **symlink** ke `~/.spck-editor/projects/{project_id}/`, yang menjaga rahasia di luar direktori proyek Anda.

### Konfigurasi Default

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### Pengaturan Browser Proxy

- **`browserProxy.enabled`** (boolean): Aktifkan/nonaktifkan fitur browser proxy
  - Default: `true`
  - Setel ke `false` untuk mencegah aplikasi mobile membuka sesi browser proxy melalui CLI

### Pengaturan Terminal

- **`terminal.enabled`** (boolean): Aktifkan/nonaktifkan akses terminal
  - Default: `true`
  - Setel ke `false` untuk mengurangi risiko akses tidak sah ke terminal Anda

- **`terminal.maxBufferedLines`** (number): Buffer scrollback maksimum
  - Default: `10000`
  - Memengaruhi penggunaan memori (~1MB per 10k baris)

- **`terminal.maxTerminals`** (number): Jumlah sesi terminal bersamaan maksimum
  - Default: `10`
  - Setiap terminal menggunakan ~5-10MB memori

### Pengaturan Filesystem

- **`filesystem.maxFileSize`** (string): Ukuran file maksimum untuk baca/tulis
  - Default: `"10MB"`
  - Menerima: `"5MB"`, `"50MB"`, dll.

- **`filesystem.watchIgnorePatterns`** (string[]): Pola yang dikecualikan dari pemantauan file
  - Default: Mengabaikan output build dan dependensi
  - Meningkatkan performa dengan menghindari ribuan file yang dihasilkan

### Pengaturan Keamanan

- **`security.userAuthenticationEnabled`** (boolean): Aktifkan autentikasi pengguna Firebase
  - Default: `false`
  - Saat `false`: Latensi lebih rendah, kompatibel dengan Lite, tetap dilindungi oleh penandatanganan rahasia
  - Saat `true`: Lapisan keamanan ekstra, verifikasi identitas pengguna, menambahkan latensi awal 2-20 detik
  - **Semua permintaan selalu ditandatangani secara kriptografis terlepas dari pengaturan ini**

## <a name="security"></a>Keamanan

### Koneksi Terenkripsi

Semua komunikasi menggunakan:

- **WSS (WebSocket Secure)**: Enkripsi TLS/SSL
- **HTTPS**: Handshake awal yang terenkripsi

### Penandatanganan Permintaan

Setiap permintaan ditandatangani secara kriptografis:

- Kunci rahasia dihasilkan secara lokal, tidak pernah dikirimkan melalui internet
- Disarankan untuk tidak menggunakan pemindai QR pihak ketiga yang mungkin mengekspos kunci rahasia Anda

### Praktik Terbaik

1. **Lindungi kredensial**:

   ```bash
   # Add to .gitignore (automatic during setup)
   echo ".spck-editor/" >> .gitignore
   ```

2. **Logout di mesin bersama**:

   ```bash
   spck --logout
   ```

3. **Batasi direktori yang diekspos**:

   ```bash
   # Instead of entire home directory
   spck --root /path/to/specific/project
   ```

4. **Nonaktifkan terminal jika tidak diperlukan**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **Nonaktifkan browser proxy jika tidak diperlukan**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>Autentikasi Pengguna

Spck CLI mendukung autentikasi pengguna Firebase opsional sebagai lapisan keamanan kedua di atas penandatanganan permintaan yang selalu aktif.

### Cara Kerjanya

Saat diaktifkan, CLI mengharuskan Anda masuk dengan akun Spck Editor Anda. Koneksi diautentikasi menggunakan token ID Firebase yang kedaluwarsa setiap jam dan diperbarui secara otomatis menggunakan token refresh aman yang disimpan di `~/.spck-editor/.credentials.json`.

### Mengaktifkan Autentikasi Pengguna

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### Pertukaran

|                       | Dinonaktifkan (default)        | Diaktifkan                              |
| --------------------- | ------------------------------ | --------------------------------------- |
| **Perlindungan**      | Kunci penandatanganan rahasia  | + Verifikasi identitas Firebase         |
| **Latensi awal**      | Tidak ada overhead autentikasi | Menambahkan 2–20 detik saat pertama kali terhubung |
| **Spck Editor Lite**  | ✅ Didukung                   | ❌ Tidak didukung                       |
| **Penggunaan offline**| Bekerja tanpa internet         | Memerlukan internet untuk pembaruan token |

### Kapan Mengaktifkan

**Tetap dinonaktifkan (default) ketika:**

- Menggunakan **Spck Editor Lite** — Login Firebase tidak didukung di Lite; menyetel ini ke `true` akan mencegah pengguna Lite terhubung
- Bekerja di jaringan lokal atau lingkungan tepercaya di mana kunci penandatanganan rahasia sudah cukup
- Meminimalkan latensi koneksi adalah prioritas

**Aktifkan ketika:**

- CLI diekspos pada server yang dapat diakses melalui internet
- Anda menginginkan verifikasi identitas pengguna sebagai lapisan kontrol akses tambahan di luar kunci penandatanganan

> ⚠️ **Spck Editor Lite tidak mendukung autentikasi Firebase.** Jika `userAuthenticationEnabled` disetel ke `true`, Spck Editor Lite tidak dapat terhubung. Pertahankan pengaturan ini di `false` saat menggunakan Lite.
