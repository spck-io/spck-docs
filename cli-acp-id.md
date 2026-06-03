# <a name="ai-coding-agents-acp"></a>Agen Pemrograman AI di Ponsel (ACP)

Jalankan **Claude Code**, **OpenAI Codex**, atau **Gemini CLI** langsung dari ponsel Anda melalui **AI Chat** Spck Editor. Spck CLI menghubungkan editor Anda ke CLI agen yang terinstal lokal melalui [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) yang terbuka, sehingga model berjalan di mesin Anda, dengan langganan Anda, terhadap file asli Anda — sambil Anda mengawasinya dari perangkat mobile.

![Mode AI lokal ACP di AI Chat Spck Editor, menjalankan Claude Code di desktop dari ponsel](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>Apa Itu ACP dan Mengapa Menggunakannya?

Agent Client Protocol (ACP) adalah standar terbuka dari Zed Industries untuk komunikasi editor ↔ agen AI, dengan semangat yang sama seperti Language Server Protocol (LSP). Spck CLI 0.6.0+ mengimplementasikan ACP dan bertindak sebagai **transport** antara AI Chat Spck Editor (klien) dan binary agen kompatibel ACP apa pun yang telah Anda instal (agen).

Dibandingkan dengan AI Chat yang dialihkan melalui server di dalam aplikasi, jalur ACP lokal memberi Anda:

- **Langganan Anda sendiri** — panggilan agen ditagihkan ke akun Claude Code / ChatGPT / Gemini Anda, bukan ke kuota AI Spck Editor Anda.
- **Akses file system nyata** — agen membaca dan menulis file asli pada disk melalui CLI, bukan salinan in-memory editor.
- **Tool native** — file watcher, language server, dan perintah shell berjalan di mesin asli Anda.
- **Kontinuitas dengan desktop** — login `claude` / `gemini` / `codex` yang sama yang Anda gunakan di meja kerja menggerakkan chat mobile.

## <a name="acp-supported-agents"></a>Agen AI yang Didukung

Instal agen mana pun yang Anda ingin tersedia. Spck CLI mendeteksinya secara otomatis saat startup.

| Agen              | Instalasi                                                                            |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>Instalasi dan Pengaturan

### 1. Instal Spck CLI

Jika Anda belum memilikinya:

```bash
npm install -g spck
# atau jalankan tanpa menginstal
npx spck
```

Lihat [Memulai dengan Spck CLI](./cli-start) untuk wizard first-run lengkap.

### 2. Instal satu atau lebih CLI agen

Pilih agen mana pun yang Anda ingin tersedia. Anda dapat menginstal beberapa — AI Chat akan membiarkan Anda memilih di antaranya per sesi. Lihat tabel [Agen AI yang Didukung](#acp-supported-agents) di atas untuk perintah instalasi.

### 3. Otentikasi setiap agen sekali

CLI agen masing-masing mengelola login mereka sendiri di luar Spck Editor:

```bash
claude            # Alur login Anthropic Claude Code
codex login       # Alur login OpenAI Codex (digunakan oleh codex-acp)
gemini            # Alur login Google Gemini
```

Jika Anda melewati langkah ini, Spck Editor akan menampilkan error seperti `ACP agent requires authentication; run <binary> login and retry` saat pertama kali Anda memulai chat.

### 4. Mulai Spck CLI

```bash
cd /path/to/your/project
spck
```

Saat startup, CLI mencetak laporan deteksi per-agen yang mencantumkan agen mana yang tersedia, diikuti dengan ringkasan satu baris seperti `✅ ACP agents: Claude Code, Gemini CLI` di blok fitur utama. Jika tidak ada yang tersedia, sistem akan beralih kembali ke AI Chat yang dialihkan melalui server.

### 5. Hubungkan Spck Editor

Pindai kode QR atau gunakan [Entri Manual](./cli-start#connecting). Setelah terhubung, buka **AI Chat** di Spck Editor — pengalih transport akan menampilkan agen lokal di samping opsi cloud.

## <a name="acp-authentication"></a>Otentikasi

Setiap agen mengelola kredensialnya sendiri di mesin tempat Spck CLI berjalan. Jalankan alur login sekali per agen:

```bash
# Claude Code
claude

# Codex (codex-acp membungkus login CLI Codex sendiri)
codex login

# Gemini CLI
gemini
```

Jika Anda menginstal ulang atau pindah mesin, ulangi login di host baru. Otentikasi dilakukan **per-host, per-agen** — Spck Editor sendiri tidak pernah menyimpan kredensial ini.

## <a name="acp-billing"></a>Penagihan dan Batas Penggunaan

Karena ACP menjalankan agen di mesin Anda dengan kredensial Anda sendiri, **semua penggunaan ditagihkan ke akun Anda dengan penyedia tersebut** — bukan ke langganan Spck Editor Anda. Spck Editor dan server relay Spck bertindak sebagai pure transport dalam mode ini dan tidak mengonsumsi kuota AI in-app Anda untuk lalu lintas ACP.

### Penagihan Claude Code

> ⚠️ **Penting — Claude Code menerapkan bucket batas penggunaan terpisah ketika digerakkan oleh tool pihak ketiga.**
>
> Ketika Claude Code dipanggil dari klien pihak ketiga melalui ACP, Anthropic menghitung lalu lintas tersebut terhadap **bucket batas penggunaan yang berbeda** dari sesi CLI `claude` interaktif Anda pada langganan Pro / Max. Konsekuensi praktisnya: Anda bisa menghabiskan bucket pihak ketiga sambil masih memiliki ruang Claude Code interaktif (atau sebaliknya), dan Anda tidak dapat menggabungkannya.

> Periksa `/usage` di dalam `claude` dan [Anthropic Console](https://platform.claude.com/usage) untuk melihat konsumsi Anda saat ini, dan tinjau [dokumentasi biaya & batas Claude Code](https://code.claude.com/docs/en/costs) untuk angka yang berlaku untuk paket Anda.

### Penagihan Codex (codex-acp)

Ditagih melalui auth milik OpenAI Codex CLI sendiri — kunci API OpenAI atau login ChatGPT Anda. Penggunaan dihitung terhadap paket apa pun yang dimiliki akun tersebut. Harga dan kuota sama dengan penggunaan `codex` interaktif; lihat [openai.com/codex](https://github.com/openai/codex) dan dashboard OpenAI Anda untuk angka terkini.

### Penagihan Gemini CLI

Ditagih melalui akun Google atau kunci API Gemini Anda. Penggunaan dihitung terhadap paket Gemini atau kuota API yang terikat ke login tersebut. Lihat [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) untuk detail batas penggunaan.

## <a name="acp-configuration"></a>Konfigurasi

ACP diaktifkan secara default dan dikonfigurasi melalui `spck-cli.config.json` proyek:

```json
{
  "acp": {
    "enabled": true
  }
}
```

Lihat [Konfigurasi → Pengaturan ACP](./cli-config#acp-settings) untuk skema lengkap.

### Nonaktifkan ACP per proyek

Jika Anda tidak ingin Spck Editor dapat menggerakkan agen lokal di host ini:

```json
{
  "acp": {
    "enabled": false
  }
}
```

Saat dinonaktifkan, pengalih transport editor menyembunyikan opsi agen lokal dan RPC `acp.*` apa pun ditolak dengan `FEATURE_DISABLED`. Wizard pengaturan menanyakan pertanyaan ini saat first run (default `Y`); konfigurasi yang mendahului opsi ini dimuat dengan `acp.enabled: true` ditambahkan secara otomatis dan disimpan ulang.

### Nonaktifkan satu agen

Untuk mencegah agen _tertentu_ ditawarkan sambil tetap mengaktifkan ACP untuk yang lain, copot pemasangan binary agen tersebut. Deteksi berjalan setiap kali CLI dimulai, sehingga pengalih transport editor akan menghapusnya dari daftar.

## <a name="acp-vs-server-routed"></a>ACP Lokal vs. AI Chat yang Dialihkan Melalui Server

| Kapabilitas                                | Dialihkan Melalui Server (default, tanpa CLI) | Lokal (ACP, CLI terhubung)              |
| ------------------------------------------ | --------------------------------------------- | --------------------------------------- |
| Di mana model dijalankan                   | Cloud Spck                                    | Mesin Anda                              |
| Kredensial                                 | Akun Spck Editor Anda                         | Login / kunci API milik agen sendiri    |
| Akses file                                 | File system in-memory editor                  | File asli pada disk melalui root CLI    |
| Dihitung terhadap kuota AI Spck Editor     | Ya                                            | **Tidak** — ditagih ke penyedia agen    |
| Berfungsi tanpa CLI berjalan               | Ya                                            | Tidak (memerlukan CLI + WebSocket)      |
| Agen yang tersedia                         | Model yang di-host Spck                       | Claude Code, Codex, Gemini CLI          |
| Prompt izin penggunaan tool di ponsel      | Jika berlaku                                  | Ya, diteruskan melalui ACP              |
| Streaming token                            | Ya                                            | Ya                                      |
| Chat multi-turn                            | Ya                                            | Ya                                      |

Anda dapat berpindah transport di tengah proyek — AI Chat menampilkan jalur mana pun yang saat ini tersedia berdasarkan status koneksi CLI dan agen yang terdeteksi.

## <a name="acp-tmux"></a>Memadukan dengan Tmux untuk Sesi Jangka Panjang

Sesi ACP tetap hidup melintasi reconnect editor, tetapi proses Spck CLI itu sendiri berakhir ketika terminalnya ditutup. Untuk pekerjaan agen jangka panjang — refactoring besar, sesi perencanaan multi-jam — mulai CLI di dalam sesi [tmux](./tmux) agar bertahan dari putus SSH, penutupan terminal, dan sleep laptop:

```bash
tmux new -s spck
spck
# Ctrl+B lalu D untuk detach
```

Anda juga dapat menyambung kembali dari ponsel Anda melalui terminal Spck CLI dan `tmux attach -t spck` untuk memantau agen secara live. Lihat [Menggunakan Tmux](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) untuk pola lengkap, termasuk menjalankan CLI sebagai layanan background persisten.

Untuk host Linux, halaman [Claude Skill: Linux Service](./claude-skill) menyediakan pengaturan satu perintah untuk menjalankan Spck CLI sebagai layanan `systemd`, sehingga WebSocket — dan sesi ACP apa pun di atasnya — auto-start saat boot.

## <a name="acp-faq"></a>Pertanyaan yang Sering Diajukan

### Bisakah saya menggunakan Claude Code di ponsel saya?

Ya. Instal Claude Code di desktop Anda, otentikasi dengan `claude`, lalu jalankan `spck` di proyek Anda. Hubungkan Spck Editor dari ponsel Anda dan pilih Claude Code di pengalih transport AI Chat. Model berjalan di desktop Anda dengan langganan Anda; Anda menggerakkannya dari ponsel Anda.

### Apakah Spck Editor melihat kunci API Claude / OpenAI / Gemini saya?

Tidak. Setiap CLI agen mengelola kredensialnya sendiri di mesin tempat Spck CLI berjalan. Pesan ACP di-tunnel melalui WebSocket terenkripsi antara ponsel dan CLI, tetapi token auth milik agen sendiri tidak pernah meninggalkan host Anda.

### Apakah ada biaya tambahan untuk menggunakan Claude Code melalui Spck Editor?

Tidak ada biaya tambahan Spck Editor. Penggunaan agen dihitung terhadap paket Anthropic / OpenAI / Google Anda persis seperti jika Anda menjalankan agen secara interaktif di meja kerja Anda — kecuali Anthropic menerapkan bucket batas penggunaan terpisah untuk klien pihak ketiga; lihat [Penagihan dan Batas Penggunaan](#acp-billing) di atas.

### Apakah saya memerlukan langganan Spck Editor berbayar untuk menggunakan ACP?

Tidak. Tier gratis (koneksi CLI 30 menit/hari) cukup untuk menggerakkan agen ACP apa pun. Hanya AI Chat in-app yang dialihkan melalui server yang mengonsumsi kuota AI Spck Editor.

### Apa yang terjadi jika saya kehilangan koneksi Wi-Fi di tengah chat?

Proses agen tetap hidup di host CLI. Ketika editor terhubung kembali, sesi dilanjutkan dengan riwayat chat penuh. Output streaming yang tiba saat Anda offline akan diputar ulang saat reconnect.

### Bisakah saya menjalankan agen di server remote bukan di laptop saya?

Ya. Jalankan Spck CLI di host Linux/macOS mana pun yang dapat dijangkau — VM dev, server rumah, workstation — dan hubungkan ke sana melalui server relay. Padukan dengan [tmux](./tmux) atau [skill systemd](./claude-skill) untuk menjaga CLI tetap hidup di antara koneksi.

### Apakah ACP berfungsi dengan Spck Editor Lite?

Ya. Lalu lintas ACP menggunakan transport WebSocket yang sama dengan filesystem dan git, yang didukung Spck Editor Lite. Pastikan `security.userAuthenticationEnabled` disetel ke `false` di konfigurasi CLI Anda — auth Firebase tidak didukung di Lite. Lihat [Konfigurasi → Otentikasi Pengguna](./cli-config#user-authentication).

### Mengapa agen saya tidak muncul di AI Chat?

Periksa log startup CLI untuk baris per-agen:

- Agen tidak terdeteksi — instal (lihat [Agen AI yang Didukung](#acp-supported-agents)).
- Terdeteksi tetapi tidak ada di editor — pastikan Anda telah menyelesaikan alur login milik agen sendiri (`claude`, `codex login`, `gemini`).
- ACP dinonaktifkan — periksa `acp.enabled` di `.spck-editor/config/spck-cli.config.json`. Lihat [Konfigurasi](./cli-config#acp-settings).

## <a name="acp-troubleshooting"></a>Pemecahan Masalah

### Agen terdeteksi tetapi sesi tidak mulai

Paling sering ini berarti agen tidak terotentikasi. Jalankan alur login agen di host CLI:

```bash
claude              # lalu selesaikan auth di browser
codex login
gemini
```

Jika masalah berlanjut, periksa log CLI di `.spck-editor/logs/` untuk output stderr agen, yang biasanya menunjukkan auth atau binary yang gagal.

### Error batas penggunaan selama chat

Untuk Claude Code, editor meneruskan 429 Anthropic apa adanya. Periksa [halaman penggunaan Anthropic Console](https://platform.claude.com/usage) dan [docs biaya Claude Code](https://code.claude.com/docs/en/costs) — ingat bahwa bucket batas penggunaan pihak ketiga terpisah dari alokasi `claude` interaktif Anda.

Untuk Codex dan Gemini, editor meneruskan error kuota milik penyedia sendiri. Selesaikan melalui konsol penyedia.

### CLI crash saat memulai sesi ACP

Spck CLI mencatat lalu lintas ACP ke `.spck-editor/logs/`. Pantau file log terbaru sambil mereproduksi masalah:

```bash
tail -f .spck-editor/logs/spck-*.log
```

Laporkan bug di [github.com/spck-editor](https://github.com/spck-editor) dengan cuplikan yang relevan.

### Agen membuat perubahan di luar root proyek

Agen ACP dibatasi pada direktori `root` yang dikonfigurasi CLI. Jika Anda melihat penulisan muncul di luarnya, laporkan issue — ini seharusnya tidak terjadi. Sebagai workaround, jalankan `spck --root /path/to/specific/project` untuk mempersempit cakupan lebih jauh.

## <a name="acp-see-also"></a>Lihat Juga

- [Memulai dengan Spck CLI](./cli-start) — instal, otentikasi, dan hubungkan untuk pertama kalinya
- [Referensi CLI](./cli) — server relay, alur kerja harian, batas koneksi
- [Konfigurasi → Pengaturan ACP](./cli-config#acp-settings) — opsi konfigurasi `acp.enabled`
- [Penggunaan Lanjutan](./cli-advanced) — flag CLI, beberapa proyek, tips prompt mobile
- [Menggunakan Tmux](./tmux) — menjaga sesi ACP tetap hidup melintasi reconnect
- [Claude Skill: Linux Service](./claude-skill) — menjalankan Spck CLI sebagai layanan `systemd` sehingga ACP selalu tersedia
- [Spesifikasi Agent Client Protocol](https://agentclientprotocol.com/) — standar terbuka yang diimplementasikan ACP
- [Dokumentasi Claude Code](https://docs.claude.com/en/docs/claude-code/overview)
- [Repositori Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
