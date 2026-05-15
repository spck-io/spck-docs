# <a name="cli-advanced-usage"></a>CLI の高度な使い方

## <a name="cli-commands"></a>CLI コマンド

### 基本コマンド

```bash
# CLI を起動する
spck

# セットアップウィザードを実行する
spck --setup

# アカウント情報を表示する
spck --account

# ログアウトして認証情報を削除する
spck --logout

# ヘルプを表示する
spck --help

# バージョンを表示する
spck --version
```

### 高度なオプション

```bash
# カスタム設定ファイルを使用する
spck --config /path/to/config.json
spck -c /path/to/config.json

# ルートディレクトリを上書きする
spck --root /path/to/project
spck -r /path/to/project

# リレーサーバーを上書きする（例: 特定のリージョンを使用する）
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>AI コーディングエージェント

Spck CLI ターミナルはフルシェルアクセスを提供するため、モバイルデバイスから直接 AI コーディングエージェントを実行できます。これらのエージェントはプロジェクトのコードを読み書き・リファクタリングしながら、Spck Editor から監視することができます。

> 💡 **ヒント**: **tmux** を使用すると、切断後も AI エージェントセッションを継続できます。デスクトップで tmux セッションを開始し（`tmux new -s code`）、AI エージェントを起動してから、スマートフォンの Spck CLI ターミナルで再接続します（`tmux attach -t code`）。これにより、コンテキストを失わずにデスクトップとモバイルをシームレスに切り替えられます。永続的なリモートサーバーのセットアップを含む完全なガイドは [tmux の使い方](./tmux) を参照してください。

## <a name="advanced-usage"></a>高度な使い方

### 複数プロジェクト

異なるプロジェクト向けに別々の CLI インスタンスを同時実行する:

```bash
# ターミナル 1: プロジェクト A
cd /path/to/projectA
spck

# ターミナル 2: プロジェクト B
cd /path/to/projectB
spck
```

各プロジェクトは独自の設定と接続を保持します。

> 💡 **ヒント**: 複数の CLI インスタンスを使用してデスクトップとスマートフォン間でファイルを転送することもできます。ステップバイステップのガイドは [モバイルとデスクトップ間のファイル転送](./cli-file-transfer) を参照してください。

### カスタム設定ファイル

異なるシナリオ向けに特化した設定を作成する:

```bash
# 開発用設定
spck --config ~/configs/dev-config.json

# 本番用設定（読み取り専用、ターミナルなし）
spck --config ~/configs/prod-config.json
```

### 環境別のセットアップ

**ローカル開発:**

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

**本番サーバー:**

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

### CPU 使用率が高い場合

無視パターンを追加してファイル監視を減らす:

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

同時ターミナル数を制限する:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>モバイル向けシェルプロンプトの短縮

モバイルデバイスでは水平方向の画面スペースが限られています。デフォルトのシェルプロンプト（通常、現在のディレクトリパス、ユーザー名、ホスト名を含む）はターミナルを圧迫し、コマンド出力が読みにくくなります。

プロンプトを `$ ` だけにすると、小さな画面でもすっきりとしたターミナル体験が得られます。

### Bash

`~/.bashrc` に以下を追加する:

```bash
export PS1='\$ '
```

シェルを再起動せずに適用する:

```bash
source ~/.bashrc
```

### Zsh

`~/.zshrc` に以下を追加する:

```zsh
PROMPT='$ '
```

シェルを再起動せずに適用する:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

プロファイルファイルがまだ存在しない場合は作成し、開く:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

プロファイルに以下を追加する:

```powershell
function prompt { "$ " }
```

シェルを再起動せずに適用する:

```powershell
. $PROFILE
```

### コマンドプロンプト (Windows)

現在のセッション用に最小限のプロンプトを設定する:

```cmd
PROMPT $$
```

永続的にするには、**コントロールパネル → システム → システムの詳細設定 → 環境変数** から `PROMPT` を値 `$$` の**ユーザー**または**システム**環境変数として追加してください。
