# <a name="tmux"></a>Menggunakan Tmux dengan Spck CLI

Tmux (Terminal Multiplexer) memungkinkan sesi terminal berjalan secara independen dari jendela atau koneksi SSH yang memulainya. Bagi pengguna Spck CLI, ini berarti Anda dapat menjaga sesi tetap aktif saat koneksi terputus, berbagi sesi agen yang sedang berjalan antara desktop dan perangkat mobile, serta menjalankan CLI secara persisten di server jarak jauh meskipun koneksi SSH Anda terputus.

## <a name="installation"></a>Instalasi

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux berjalan secara native di Linux. Di Windows, gunakan [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install), lalu instal tmux di dalam WSL.

**Langkah 1 — Instal WSL (PowerShell sebagai Administrator):**

```powershell
wsl --install
```

**Langkah 2 — Buka terminal WSL dan instal tmux:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>Kasus Penggunaan 1: Berbagi Sesi Agen Antara Desktop dan Mobile

Alur kerja tmux paling powerful bersama Spck CLI adalah memulai agen coding AI di desktop Anda dan melanjutkannya secara mulus dari perangkat mobile — atau sebaliknya. Keduanya melihat kondisi terminal yang persis sama termasuk riwayat gulir lengkap.

### Memulai Sesi di Desktop

Buat sesi tmux bernama:

```bash
tmux new -s code
```

Jalankan agen AI di dalam sesi:

```bash
claude
```

Agen berjalan di dalam tmux. Lepaskan koneksi kapan saja dengan menekan **Ctrl+B** lalu **D** — sesi dan semua yang berjalan di dalamnya terus berjalan di latar belakang.

### Menghubungkan dari Mobile

1. Buka Spck Editor dan hubungkan ke server CLI Anda
2. Buka terminal dari panel terminal Spck Editor
3. Hubungkan ke sesi tmux yang sedang berjalan:

```bash
tmux attach -t code
```

Anda melihat terminal yang persis sama seperti di desktop — termasuk agen yang berjalan, outputnya, dan riwayat gulir lengkap. Beberapa klien dapat terhubung secara bersamaan dan melihat output langsung.

### Kembali ke Desktop

Hubungkan kembali dari terminal mana pun kapan saja:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>Kasus Penggunaan 2: CLI Persisten di Server Jarak Jauh

Jika Anda menjalankan Spck CLI di server jarak jauh melalui SSH, CLI akan berhenti saat sesi SSH berakhir — baik karena Anda menutup laptop, kehilangan Wi-Fi, maupun koneksi yang timeout. Tmux menjaga proses tetap berjalan di server terlepas dari kondisi koneksi Anda.

### Pengaturan di Server Jarak Jauh

SSH ke server Anda dan mulai sesi tmux bernama sebelum menjalankan CLI:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

CLI sekarang berjalan di dalam tmux di server. Tutup koneksi SSH — atau putuskan sepenuhnya — dan CLI tetap berjalan.

### Menghubungkan Kembali Setelah Terputus

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLI melanjutkan tepat di mana ia berhenti. Klien mobile dapat terhubung kembali melalui server relay seperti biasa.

### Menampilkan Daftar Sesi yang Berjalan

```bash
tmux ls
```

## <a name="linux-service"></a>Alternatif: Layanan Linux

Untuk pengaturan yang sepenuhnya otomatis yang memulai CLI saat boot tanpa manajemen tmux manual apa pun, jalankan Spck CLI sebagai layanan systemd.

### Membuat File Layanan

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Ganti `your-username` dan `/path/to/your/project` dengan nilai Anda yang sebenarnya. Jika Anda menginstal `spck` secara global (`npm install -g spck`), ganti `ExecStart` dengan output dari `which spck`.

### Mengaktifkan dan Memulai

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### Memeriksa Status dan Log

```bash
# Lihat status
sudo systemctl status spck-cli

# Ikuti log langsung
journalctl -u spck-cli -f
```

Layanan mulai otomatis setiap kali reboot dan memulai ulang sendiri jika proses mengalami crash.

## <a name="essential-tmux-commands"></a>Perintah Tmux Penting

| Perintah | Aksi |
| --- | --- |
| `tmux new -s name` | Membuat sesi bernama baru |
| `tmux attach -t name` | Menghubungkan ke sesi yang sudah ada |
| `tmux ls` | Menampilkan semua sesi |
| `tmux kill-session -t name` | Menghentikan sesi |
| Ctrl+B, D | Melepaskan dari sesi (tetap berjalan) |
| Ctrl+B, C | Membuat jendela baru |
| Ctrl+B, N | Beralih ke jendela berikutnya |
| Ctrl+B, P | Beralih ke jendela sebelumnya |
| Ctrl+B, [ | Masuk mode gulir (tombol panah / PgUp / PgDn) |
| Q | Keluar dari mode gulir |
