# <a name="claude-skill"></a>Claude Skill: Menjalankan Spck CLI sebagai Layanan Linux

Halaman ini menyediakan [skill Claude Code](https://docs.claude.com/en/docs/claude-code/skills) yang dapat diunduh untuk mengotomatiskan pemasangan Spck CLI (`spck`) sebagai layanan `systemd` di Linux. Dengan skill yang terpasang, Anda dapat meminta Claude Code untuk "menjalankan spck sebagai layanan" dan ia akan memeriksa lingkungan Anda, menghasilkan file unit yang benar dengan jalur absolut Anda, memasangnya, dan memverifikasi bahwa ia berjalan — tanpa perlu menyalin-tempel perintah dari sebuah daftar.

Skill ini mengkodekan pengaturan systemd yang sama seperti yang dijelaskan di [Menggunakan Tmux → Alternatif: Layanan Linux](./tmux#linux-service), ditambah pemeriksaan awal dan diagnostik kegagalan yang mudah terlewat saat menulis file unit secara manual.

## <a name="download"></a>Unduh

Unduh file skill dan simpan ke direktori skills Claude Code lokal Anda:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

Atau unduh secara manual: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — tempatkan di `~/.claude/skills/spck-cli-service/SKILL.md`.

## <a name="what-the-skill-does"></a>Apa yang Dilakukan Skill

Saat dipanggil, skill memandu Claude Code melalui instalasi lengkap:

1. Memverifikasi bahwa host adalah Linux yang menjalankan `systemd`.
2. Menyelesaikan jalur absolut ke `spck` (menghindari ketidakcocokan `PATH` yang merusak `ExecStart`).
3. Memperingatkan jika `node` diinstal melalui `nvm` — jalur tersebut berubah setiap peningkatan Node dan merusak unit secara diam-diam.
4. Mengonfirmasi bahwa `~/.spck-editor/.credentials.json` ada (CLI harus dijalankan secara interaktif setidaknya sekali sebelum berjalan sebagai layanan).
5. Memilih antara **layanan pengguna** (`systemctl --user`, tanpa `sudo`) dan **layanan sistem** berdasarkan kebutuhan Anda.
6. Menulis file unit dengan jalur nyata Anda yang sudah diisi — tanpa placeholder.
7. Menjalankan `daemon-reload`, `enable --now`, lalu mengikuti journal untuk mengonfirmasi bahwa CLI terhubung ke server relay.

Skill juga mendokumentasikan tujuh mode kegagalan paling umum (jalur `ExecStart` yang salah, kredensial yang hilang, kesalahan izin pada direktori proyek, loop restart yang mencapai `start-limit-hit`, jalur nvm yang kedaluwarsa setelah peningkatan npm, dll.) sehingga Claude Code dapat mendiagnosis layanan yang rusak daripada sekadar meregenerasi file unit.

## <a name="installation"></a>Instalasi

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**Langkah 1 — Unduh file skill:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**Langkah 2 — Verifikasi bahwa Claude Code mendeteksinya:**

```bash
claude /skills
```

Anda seharusnya melihat `spck-cli-service` dalam daftar. Jika tidak, mulai ulang Claude Code agar ia memindai ulang direktori skills.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop memuat skills dari direktori `~/.claude/skills/` yang sama di macOS dan Linux. Di Windows, jalurnya adalah `%USERPROFILE%\.claude\skills\` — tetapi skill itu sendiri hanya berfungsi di host Linux, jadi instal di mesin tempat Anda ingin menjalankan `spck`, bukan di mesin yang menjalankan Claude Desktop.

Jika Anda mengelola server Linux jarak jauh, jalankan Claude Code melalui SSH di server tersebut (atau melalui terminal Spck CLI, yang mengekspos shell penuh ke server). Menginstal skill di Mac lokal tidak akan membantu mengonfigurasi layanan Linux jarak jauh.

</div>
  </div>
</div>

## <a name="usage"></a>Penggunaan

Setelah terpasang, panggil skill dengan meminta Claude Code dalam bahasa biasa. Contoh yang akan memicunya:

- "Instal spck sebagai layanan systemd"
- "Buat Spck CLI mulai saat boot"
- "spck-cli.service saya terus restart, bisakah kamu debug?"
- "Jalankan spck sebagai daemon agar bertahan saat SSH terputus"

Claude Code akan membaca skill, menjalankan pemeriksaan awal (yang akan meminta Anda menyetujui setiap perintah), lalu menghasilkan dan memasang file unit. Tinjau setiap perintah sebelum menyetujui — terutama yang menulis ke `/etc/systemd/system/` dengan `sudo`.

## <a name="what-gets-installed"></a>Apa yang Dipasang

Skill memasang satu file unit. Untuk layanan pengguna, filenya berada di:

```bash
~/.config/systemd/user/spck-cli.service
```

Dengan konten seperti:

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

Untuk layanan sistem, file berada di `/etc/systemd/system/spck-cli.service` dan menambahkan direktif `User=` dan `Group=`. Skill memilih varian yang tepat berdasarkan lingkungan Anda dan mengisi jalur absolut nyata ke dalam file.

## <a name="why-a-skill-instead-of-copy-paste"></a>Mengapa Skill daripada Salin-Tempel?

File unit di [dokumentasi tmux](./tmux#linux-service) adalah titik awal, tetapi beberapa hal harus benar agar layanan benar-benar berfungsi:

- `ExecStart` harus berupa **jalur absolut** ke `spck`. `which spck` di dalam login shell akan menyelesaikan manipulasi PATH dari `.bashrc` yang tidak dilihat oleh systemd.
- Jika `spck` diinstal di bawah `nvm`, jalurnya menyematkan versi Node — memperbarui Node merusak layanan secara diam-diam hingga reboot berikutnya.
- CLI harus pernah dijalankan secara interaktif setidaknya sekali untuk membuat `~/.spck-editor/.credentials.json`. Start layanan baru tanpa kredensial berakhir dengan bersih tanpa error yang jelas.
- `User=` harus memiliki `WorkingDirectory`, jika tidak pemantauan file akan mendapat `EACCES` dan CLI akan masuk ke loop restart.
- Layanan pengguna membutuhkan `loginctl enable-linger` di server tanpa layar, jika tidak mereka hanya berjalan selama sesi login aktif.

Skill mengkodekan semua ini sehingga Anda tidak perlu mengingatnya.

## <a name="uninstall"></a>Menghapus Instalasi

Nonaktifkan dan hapus layanan:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

Untuk layanan sistem:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Untuk menghapus skill itu sendiri dari Claude Code:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>Lihat Juga

- [Menggunakan Tmux](./tmux) — pendekatan alternatif menggunakan `tmux` untuk menjaga CLI tetap berjalan saat SSH terputus.
- [Penggunaan Lanjutan](./cli-advanced) — referensi perintah CLI lengkap, penggantian konfigurasi, dan pengaturan multi-proyek.
- [Konfigurasi](./cli-config) — pengaturan terminal, sistem file, keamanan, dan autentikasi yang tidak dicakup file unit.
