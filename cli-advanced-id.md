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

## <a name="ai-coding-agents"></a>Agen Coding AI (ACP)

Spck CLI menjembatani AI Chat Spck Editor ke agen coding AI yang terinstal secara lokal — **Claude Code**, **Codex**, atau **Gemini CLI** — melalui [Agent Client Protocol (ACP)](https://agentclientprotocol.com/). Model berjalan di mesin Anda dengan langganan Anda sendiri, mengedit file nyata di disk, dan meneruskan permintaan izin ke ponsel Anda.

![Mode AI lokal di AI Chat Spck Editor menjalankan Claude Code dari ponsel](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[Agen AI Coding di Mobile (ACP)](./cli-acp)** — panduan lengkap: agen yang didukung, instalasi, penagihan & batas laju (termasuk kuota Claude Code pihak ketiga terpisah dari Anthropic), konfigurasi, FAQ, dan pemecahan masalah.

> 💡 **Tips**: Gunakan **tmux** agar sesi agen AI tetap berjalan bahkan setelah Anda memutuskan koneksi. Mulai sesi tmux di desktop (`tmux new -s code`), luncurkan agen, lalu sambungkan kembali dari terminal Spck CLI di ponsel Anda (`tmux attach -t code`). Bekerja untuk agen shell biasa maupun agen mode ACP. Lihat [Menggunakan Tmux](./tmux) untuk panduan lengkap termasuk pengaturan server remote persisten.

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
