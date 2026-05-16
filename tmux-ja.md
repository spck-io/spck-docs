# <a name="tmux"></a>Spck CLI で Tmux を使う

Tmux（ターミナルマルチプレクサー）を使うと、ターミナルセッションをそれを起動したウィンドウやSSH接続から独立して実行し続けることができます。Spck CLIユーザーにとっては、再接続をまたいでセッションを維持したり、実行中のエージェントセッションをデスクトップとモバイルの間で共有したり、SSHセッションが切れた後もリモートサーバーでCLIを継続実行したりできることを意味します。

## <a name="installation"></a>インストール

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

TmuxはLinux上でネイティブに動作します。Windowsでは[Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)を使用し、WSL内にtmuxをインストールしてください。

**手順1 — WSLをインストールする（管理者としてPowerShellを実行）:**

```powershell
wsl --install
```

**手順2 — WSLターミナルを開いてtmuxをインストールする:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>ユースケース1: デスクトップとモバイル間でエージェントセッションを共有する

Spck CLIとtmuxを組み合わせた最も強力なワークフローは、デスクトップでAIコーディングエージェントを起動し、モバイルからシームレスに引き継ぐことです（またはその逆）。どちらも完全なスクロールバック履歴を含む、まったく同じターミナル状態を見ることができます。

### デスクトップでセッションを開始する

名前付きtmuxセッションを作成します:

```bash
tmux new -s code
```

セッション内でAIエージェントを起動します:

```bash
claude
```

エージェントはtmux内で実行されます。**Ctrl+B** を押してから **D** を押すといつでもデタッチできます — セッションとその中で実行されているものはすべてバックグラウンドで継続します。

### モバイルから接続する

1. Spck Editorを開き、CLIサーバーに接続します
2. Spck Editorのターミナルパネルからターミナルを開きます
3. 実行中のtmuxセッションにアタッチします:

```bash
tmux attach -t code
```

デスクトップとまったく同じターミナルが表示されます — 実行中のエージェント、その出力、完全なスクロールバック履歴も含めて。複数のクライアントが同時にアタッチしてライブ出力を見ることができます。

### デスクトップに戻る

いつでも任意のターミナルから再接続できます:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>ユースケース2: リモートサーバーで継続的にCLIを実行する

SSHでリモートサーバー上でSpck CLIを実行している場合、SSHセッションが終了した瞬間にCLIも停止します — ラップトップを閉じても、Wi-Fiが切れても、タイムアウトしても同様です。Tmuxは接続状態に関わらずサーバー上でプロセスを実行し続けます。

### リモートサーバーでの設定

サーバーにSSH接続し、CLIを起動する前に名前付きtmuxセッションを開始します:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

CLIがサーバー上のtmux内で実行されます。SSH接続を閉じても、完全に切断されても、CLIは実行し続けます。

### 切断後に再接続する

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLIは中断したところからそのまま再開します。モバイルクライアントはリレーサーバー経由で通常通り再接続できます。

### 実行中のセッションを一覧表示する

```bash
tmux ls
```

## <a name="linux-service"></a>代替手段: Linuxサービス

tmuxの手動管理なしに起動時に自動でCLIを開始する完全自動化されたセットアップには、Spck CLIをsystemdサービスとして実行します。

### サービスファイルを作成する

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

`your-username` と `/path/to/your/project` を実際の値に置き換えてください。`spck` をグローバルインストールした場合（`npm install -g spck`）、`ExecStart` を `which spck` の出力に置き換えてください。

### 有効化して起動する

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### ステータスとログを確認する

```bash
# ステータスを確認
sudo systemctl status spck-cli

# ライブログを追跡
journalctl -u spck-cli -f
```

サービスは再起動のたびに自動的に起動し、プロセスがクラッシュした場合は自動的に再起動します。

## <a name="essential-tmux-commands"></a>主要なTmuxコマンド

| コマンド | 操作 |
| --- | --- |
| `tmux new -s name` | 名前付きセッションを作成 |
| `tmux attach -t name` | 既存のセッションに接続 |
| `tmux ls` | すべてのセッションを一覧表示 |
| `tmux kill-session -t name` | セッションを終了 |
| Ctrl+B, D | セッションからデタッチ（実行を継続） |
| Ctrl+B, C | 新しいウィンドウを作成 |
| Ctrl+B, N | 次のウィンドウに切り替え |
| Ctrl+B, P | 前のウィンドウに切り替え |
| Ctrl+B, [ | スクロールモードに入る（矢印キー / PgUp / PgDn） |
| Q | スクロールモードを終了 |
