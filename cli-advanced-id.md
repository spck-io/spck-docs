# <a name="cli-advanced-usage"></a>Penggunaan Lanjutan CLI

## <a name="cli-commands"></a>Perintah CLI

### Perintah Dasar

```bash
# Mulai CLI
spck

# Jalankan wizard pengaturan
spck --setup

# Tampilkan informasi akun
spck --account

# Keluar dan hapus kredensial
spck --logout

# Tampilkan bantuan
spck --help

# Tampilkan versi
spck --version
```

### Opsi Lanjutan

```bash
# Gunakan file konfigurasi kustom
spck --config /path/to/config.json
spck -c /path/to/config.json

# Ganti direktori root
spck --root /path/to/project
spck -r /path/to/project

# Ganti server relay (mis., gunakan region tertentu)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>Agen Pengkodean AI

Terminal Spck CLI memberi Anda akses shell penuh, yang berarti Anda dapat menjalankan agen pengkodean AI langsung dari perangkat mobile Anda. Agen-agen ini dapat membaca, menulis, dan merefaktor kode di proyek Anda sementara Anda mengawasi dari Spck Editor.

> 💡 **Tips**: Gunakan **tmux** agar sesi agen AI tetap berjalan bahkan setelah Anda memutuskan koneksi. Mulai sesi tmux di desktop Anda (`tmux new -s code`), luncurkan agen AI, lalu sambungkan kembali dari terminal Spck CLI di ponsel Anda (`tmux attach -t code`). Ini memungkinkan Anda beralih mulus antara desktop dan mobile tanpa kehilangan konteks. Lihat [Menggunakan Tmux](./tmux) untuk panduan lengkap termasuk pengaturan server jarak jauh yang persisten.

## <a name="advanced-usage"></a>Penggunaan Lanjutan

### Beberapa Proyek

Jalankan instans CLI terpisah untuk proyek yang berbeda secara bersamaan:

```bash
# Terminal 1: Proyek A
cd /path/to/projectA
spck

# Terminal 2: Proyek B
cd /path/to/projectB
spck
```

Setiap proyek mempertahankan konfigurasi dan koneksinya sendiri.

> 💡 **Tips**: Anda juga dapat menggunakan beberapa instans CLI untuk mentransfer file antara desktop dan ponsel Anda. Lihat [Transfer File Antara Mobile dan Desktop](./cli-file-transfer) untuk panduan langkah demi langkah.

### File Konfigurasi Kustom

Buat konfigurasi khusus untuk skenario yang berbeda:

```bash
# Konfigurasi pengembangan
spck --config ~/configs/dev-config.json

# Konfigurasi produksi (hanya baca, tanpa terminal)
spck --config ~/configs/prod-config.json
```

### Pengaturan Spesifik Lingkungan

**Pengembangan Lokal:**

```json
{
  "security": {
    "userAuthenticationEnabled": false
  },
  "terminal": {
    "enabled": true
  }
}
```

**Server Produksi:**

```json
{
  "security": {
    "userAuthenticationEnabled": true
  },
  "terminal": {
    "enabled": false
  }
}
```

### Penggunaan CPU Tinggi

Kurangi pemantauan file dengan menambahkan lebih banyak pola pengabaian:

```json
{
  "filesystem": {
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/dist/**",
      "**/build/**",
      "**/.next/**",
      "**/coverage/**",
      "**/.cache/**"
    ]
  }
}
```

Batasi terminal yang berjalan bersamaan:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>Memperkecil Prompt Shell untuk Mobile

Di perangkat mobile, ruang layar horizontal terbatas. Prompt shell default — yang biasanya mencakup jalur direktori saat ini, nama pengguna, dan nama host — dapat memenuhi terminal dan membuat output perintah lebih sulit dibaca.

Mengubah prompt Anda menjadi hanya `$ ` memberikan pengalaman terminal yang jauh lebih bersih di layar kecil.

### Bash

Tambahkan berikut ini ke `~/.bashrc`:

```bash
export PS1='\$ '
```

Terapkan tanpa memulai ulang shell:

```bash
source ~/.bashrc
```

### Zsh

Tambahkan berikut ini ke `~/.zshrc`:

```zsh
PROMPT='$ '
```

Terapkan tanpa memulai ulang shell:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

Buat file profil Anda jika belum ada, lalu buka:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

Tambahkan berikut ini ke profil:

```powershell
function prompt { "$ " }
```

Terapkan tanpa memulai ulang shell:

```powershell
. $PROFILE
```

### Command Prompt (Windows)

Atur prompt minimal untuk sesi saat ini:

```cmd
PROMPT $$
```

Untuk membuatnya permanen, tambahkan `PROMPT` sebagai variabel lingkungan **Pengguna** atau **Sistem** dengan nilai `$$` melalui **Panel Kontrol → Sistem → Pengaturan Sistem Lanjutan → Variabel Lingkungan**.
