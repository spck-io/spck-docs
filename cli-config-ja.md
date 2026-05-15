# <a name="cli-configuration"></a>CLI 設定

## <a name="configuration"></a>設定

### 設定ファイルの場所

設定はプロジェクトディレクトリ内の `.spck-editor/config/spck-cli.config.json` に保存されます。

**重要**: `.spck-editor/config` は `~/.spck-editor/projects/{project_id}/` への**シンボリックリンク**であり、シークレットをプロジェクトディレクトリの外に保持します。

### デフォルト設定

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

### ブラウザプロキシ設定

- **`browserProxy.enabled`** (boolean): ブラウザプロキシ機能の有効/無効
  - デフォルト: `true`
  - `false` に設定すると、モバイルアプリが CLI 経由でブラウザプロキシセッションを開くのを防止

### ターミナル設定

- **`terminal.enabled`** (boolean): ターミナルアクセスの有効/無効
  - デフォルト: `true`
  - `false` に設定すると、ターミナルへの不正アクセスのリスクを軽減

- **`terminal.maxBufferedLines`** (number): 最大スクロールバックバッファ
  - デフォルト: `10000`
  - メモリ使用量に影響（10,000行あたり約 1MB）

- **`terminal.maxTerminals`** (number): 最大同時ターミナルセッション数
  - デフォルト: `10`
  - 各ターミナルは約 5～10MB のメモリを使用

### ファイルシステム設定

- **`filesystem.maxFileSize`** (string): 読み取り/書き込みの最大ファイルサイズ
  - デフォルト: `"10MB"`
  - 使用可能な値: `"5MB"`、`"50MB"` など

- **`filesystem.watchIgnorePatterns`** (string[]): ファイル監視から除外するパターン
  - デフォルト: ビルド出力と依存関係を除外
  - 大量の生成ファイルを避けることでパフォーマンスを向上

### セキュリティ設定

- **`security.userAuthenticationEnabled`** (boolean): Firebase ユーザー認証の有効化
  - デフォルト: `false`
  - `false` の場合: 低レイテンシー、Lite との互換性あり、シークレット署名で保護
  - `true` の場合: 追加のセキュリティレイヤー、ユーザー認証、初回接続時に 2～20秒の遅延が発生
  - **この設定に関わらず、すべてのリクエストは常に暗号署名されます**

## <a name="security"></a>セキュリティ

### 暗号化接続

すべての通信で以下を使用：

- **WSS (WebSocket Secure)**: TLS/SSL 暗号化
- **HTTPS**: 暗号化された初期ハンドシェイク

### リクエスト署名

すべてのリクエストは暗号署名されます：

- シークレットキーはローカルで生成され、インターネット上には送信されない
- シークレットキーが漏洩する可能性があるため、サードパーティの QR スキャナーの使用は推奨しない

### ベストプラクティス

1. **認証情報を保護する**:

   ```bash
   # Add to .gitignore (automatic during setup)
   echo ".spck-editor/" >> .gitignore
   ```

2. **共有マシンからログアウトする**:

   ```bash
   spck --logout
   ```

3. **公開するディレクトリを制限する**:

   ```bash
   # Instead of entire home directory
   spck --root /path/to/specific/project
   ```

4. **不要なターミナルを無効にする**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **不要なブラウザプロキシを無効にする**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>ユーザー認証

Spck CLI は、常にアクティブなリクエスト署名に加えて、第二のセキュリティレイヤーとしてオプションの Firebase ユーザー認証をサポートしています。

### 仕組み

有効にすると、CLI は Spck Editor アカウントでのサインインを要求します。接続は、1時間ごとに期限切れとなり `~/.spck-editor/.credentials.json` に保存された安全なリフレッシュトークンを使って自動更新される Firebase ID トークンで認証されます。

### ユーザー認証の有効化

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### トレードオフ

|                          | 無効（デフォルト）             | 有効                                  |
| ------------------------ | ------------------------------ | ------------------------------------- |
| **保護**                 | シークレット署名キー           | + Firebase アイデンティティ検証       |
| **初回レイテンシー**      | 認証オーバーヘッドなし         | 初回接続時に 2～20秒の遅延            |
| **Spck Editor Lite**     | ✅ サポート対象               | ❌ 非サポート                         |
| **オフライン使用**        | インターネット不要で動作       | トークン更新にインターネットが必要     |

### 有効にするタイミング

**無効のまま（デフォルト）にすべき場合:**

- **Spck Editor Lite** を使用している場合 — Lite では Firebase ログインがサポートされていないため、`true` に設定すると Lite ユーザーは接続できなくなります
- ローカルネットワークや信頼できる環境で作業しており、シークレット署名キーで十分な場合
- 接続レイテンシーの最小化が優先事項の場合

**有効にすべき場合:**

- CLI がインターネット経由でアクセス可能なサーバーに公開されている場合
- 署名キーを超える追加のアクセス制御レイヤーとして、ユーザーアイデンティティの検証が必要な場合

> ⚠️ **Spck Editor Lite は Firebase 認証をサポートしていません。** `userAuthenticationEnabled` を `true` に設定すると、Spck Editor Lite は接続できなくなります。Lite を使用する場合は、この設定を `false` のままにしてください。
