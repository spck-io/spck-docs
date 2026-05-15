# <a name="cli-reference"></a>CLI リファレンス

## <a name="key-features"></a>主な機能

- **リモートファイルシステム**: Spck Editor モバイルアプリからローカルファイルにアクセスして編集
- **Git 統合**: 完全な Git 操作（コミット、プッシュ、プル、ブランチ管理）— Git 2.20.0 以上が必要
- **ターミナルアクセス**: xterm.js によるインタラクティブなターミナルセッション
- **ブラウザプロキシ**: Spck Editor 内のフルスクリーンブラウザビューでローカルサーバーをプレビュー
- **高速検索**: ripgrep の自動検出による最適化されたファイル検索（インストール時 100倍速）
- **セキュア**: オプションの Firebase 認証による暗号署名リクエスト

## <a name="relay-server"></a>リレーサーバー

CLI はリレーサーバーを通じて Spck Editor に接続し、両者の間でメッセージを転送します。初回起動時、CLI は最も低レイテンシーのリレーサーバーを自動的に選択し、設定を `~/.spck-editor/.credentials.json` に保存します。

**重要**: CLI と Spck Editor クライアントの両方が同じリレーサーバーを使用する必要があります。クライアントが CLI を見つけられない場合は、両側で同じリレーサーバーが選択されているか確認してください。

### 利用可能なリレーサーバー

| リージョン     | URL                 |
| ------------- | ------------------- |
| ヨーロッパ     | `cli-eu-1.spck.io`  |
| 北アメリカ     | `cli-na-1.spck.io`  |
| 南アジア       | `cli-sas-1.spck.io` |
| 東アジア       | `cli-ea-1.spck.io`  |

### リレーサーバーの上書き

```bash
# Use a specific relay server
spck --server cli-eu-1.spck.io

# Short form
spck -s cli-na-1.spck.io
```

上書き設定は保存され、次回以降の実行でも使用されます。自動選択を再実行するには、認証情報をクリアして再起動してください：

```bash
spck --logout
spck
```

### Spck Editor でのリレーサーバーの選択

モバイルアプリから **Link Remote Server** で接続する際、CLI が使用しているものと同じリレーサーバーを **Relay Server** ドロップダウンから選択してください。リレーサーバー名は接続後に CLI の出力に表示されます。

## <a name="daily-workflow"></a>日常のワークフロー

### セッションの開始

```bash
cd /path/to/project
spck
# Connect from mobile app (auto-connects to saved server)
# Start coding
```

### ファイルの編集

1. モバイルアプリでファイルを閲覧
2. タップして開いて編集
3. ファイルは自動的にコンピューターに保存

### Git コマンドの実行

**オプション 1 - モバイルアプリ GUI:**

- Git パネルを開く
- 変更を確認し、ファイルをステージング
- コミットしてプッシュ

**オプション 2 - ターミナル:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### ターミナルセッション

モバイルアプリのターミナルアイコンをタップすると、ユーザー権限でフルシェルにアクセスできます。

### セッションの終了

```bash
# Keep CLI running for quick reconnects (recommended)
# Or stop with Ctrl+C
```

## <a name="troubleshooting"></a>トラブルシューティング

### ルートディレクトリが見つからない

```bash
# Reconfigure with correct path
spck --setup

# Or specify directly
spck --root /correct/path/to/project
```

### 設定ファイルの破損

```bash
# Clear settings and start fresh
spck --logout
spck --setup
```

### 接続の問題

1. インターネット接続を確認
2. CLI と Spck Editor の両方が**同じリレーサーバー**を使用していることを確認（接続後の CLI 出力に表示）
3. ログアウトして再接続を試みる：
   ```bash
   spck --logout
   spck
   ```
4. ファイアウォール設定を確認 — WebSocket 接続（ポート 443）が許可されていることを確認

### QR コードがスキャンできない

- スキャン前に Spck Editor アプリがインストールされていることを確認
- 手動入力を使用: Projects → New Project → Link Remote Server
- サードパーティのスキャナーではなく、ネイティブのカメラアプリを使用

### Git 操作が機能しない

1. Git がインストールされていることを確認：

   ```bash
   git --version  # Requires 2.20.0+
   ```

2. 必要に応じてインストール：

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Download from git-scm.com
   ```

### 検索パフォーマンスが遅い

100倍速い検索のために ripgrep をインストール：

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI automatically detects and uses ripgrep
```

### 権限が拒否された

```bash
# View permissions
ls -la /path/to/file

# Fix if needed
chmod 644 /path/to/file

# Don't use sudo - CLI should run as the user who owns the files
```

## <a name="connection-limits"></a>接続制限

同時 CLI 接続数の上限と1日の利用制限は、アカウントの種類によって異なります：

| プラン        | CLI 接続数 | 1日の制限 |
| ------------ | ---------- | --------- |
| 無料          | 1          | 30分      |
| サポーター     | 2          | 無制限    |
| ゴールド       | 5          | 無制限    |

無料プランの利用は毎日 UTC 午前 0:00 にリセットされます。

接続制限に達した場合：

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

1日の無料プラン制限に達した場合：

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

アクティブな接続を確認：

```bash
spck --account
```

> 💡 **注意**: 1つの CLI インスタンスに接続できるモバイルデバイスは同時に1台のみです。各 CLI インスタンスは1つの接続スロットを使用します。

## <a name="support"></a>サポート

- **ウェブサイト**: [https://spck.io](https://spck.io)
- **サポート**: Spck Editor モバイルアプリからお問い合わせ
