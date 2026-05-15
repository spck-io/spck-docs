# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>概要

Spck CLI には、TypeScript、JavaScript、Python、HTML、CSS、SCSS の言語サーバーをリモートホスト上で直接実行するフル機能の Language Server Protocol (LSP) ブリッジが含まれています。CLI セッションに接続すると、Spck Editor はモバイル内蔵の言語サーバーではなく、自動的にリモート言語サーバーを使用します。

> 💡 **ヒント**: CLI なしで利用できる内蔵言語サーバーの説明については、[エディター Language Server](./editor-language-server) を参照してください。

## <a name="cli-ls-architecture"></a>アーキテクチャ

CLI 言語サーバーは、プロジェクトファイルと同じマシン上で動作します。これにより、モバイルで使用されるブラウザーベースのアプローチに比べていくつかの重要な利点があります。

### ファイル転送不要

モバイル内蔵の言語サーバーでは、言語サーバーがファイルを解析する前に、ファイルをデバイスに転送してブラウザーワーカーに読み込む必要があります。CLI では、言語サーバーがディスクから直接ファイルを読み取るため、転送は不要です。これにより帯域幅のオーバーヘッドが解消され、大規模なプロジェクトでも高速に解析できます。

### プロジェクト全体の把握

CLI 言語サーバーは、以下を含むプロジェクトディレクトリ全体にアクセスできます。

- すべてのサブディレクトリにわたるすべてのソースファイル
- サードパーティの型解決のための `node_modules/`
- 任意の深さで自動検出される `tsconfig.json` ファイル
- `.js`、`.ts`、`.d.ts`、`.jsx`、`.tsx`、`.vue` および関連する宣言ファイル

つまり、「定義へ移動」「参照を検索」「シンボルの名前変更」が、エディターでファイルを開いていない場合でも、ファイルをまたいで正しく機能します。

### 適切な `tsconfig.json` の処理

TypeScript 言語サーバーは、プロジェクトの `tsconfig.json`（または `jsconfig.json`）を自動的に検出して尊重します。パスエイリアス（`paths`）、コンパイラオプション（`strict`、`target`、`lib`）、プロジェクト参照、モノレポのワークスペースレイアウトはすべて正しく処理されます。モバイル内蔵の言語サーバーは、起動時にファイルシステムへのアクセス権がないため、`tsconfig.json` を読み取ることができません。

### 永続的なプロセス

言語サーバープロセスは、CLI セッションの間中、実行し続けます。プロジェクトのインメモリインデックスを構築し、編集間もそれを維持するため、初回起動後もレスポンスが高速なままです。

## <a name="cli-ls-features"></a>サポートされている機能

| 機能 | 説明 |
| --- | --- |
| **コード補完** | 型シグネチャ付きのコンテキスト対応の候補を関連性順に表示 |
| **ホバー情報** | カーソル下のシンボルの型情報と JSDoc ドキュメント |
| **シグネチャヘルプ** | 関数呼び出しの入力中にパラメーターのヒントとドキュメントを表示 |
| **定義へ移動** | `node_modules` 内のものを含む、任意のシンボルの宣言にジャンプ |
| **参照を検索** | プロジェクト全体でシンボルのすべての使用箇所を一覧表示 |
| **シンボルの名前変更** | シンボルの名前を変更し、すべての参照をアトミックに更新 |
| **診断** | 入力中のリアルタイムのエラーと警告のハイライト |
| **Markdown レンダリング** | ホバーとシグネチャのドキュメントをシンタックスハイライト付きコードブロックの Markdown としてレンダリング |

## <a name="cli-ls-languages"></a>サポートされている言語

| 言語 | 補完 | ホバー | シグネチャ | 診断 |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>設定

言語サーバーのサポートはデフォルトで有効になっています。設定ファイルで制御できます。

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): すべてのリモート言語サーバーのマスタースイッチ。デフォルト: `true`。
- **`languageServer.typescript.enabled`** (boolean): TypeScript/JavaScript 言語サーバーを有効にする。デフォルト: `true`。
- **`languageServer.python.enabled`** (boolean): Python 言語サーバーを有効にする（`PATH` に `pylsp` が必要）。デフォルト: `true`。

## <a name="cli-ls-requirements"></a>要件

- **TypeScript / JavaScript**: CLI に同梱されています。追加インストール不要。
- **Python**: [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) が必要です（`pip install python-lsp-server`）。
- **HTML / CSS / SCSS**: CLI に同梱されています。追加インストール不要。

## <a name="cli-ls-vs-mobile"></a>CLI vs. モバイル言語サーバー

| 機能 | CLI Language Server | モバイル内蔵 |
| --- | --- | --- |
| プロジェクトファイルへのフルアクセス | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| `node_modules` の型解決 | ✓ | — |
| ファイルをまたいだ定義へ移動 | ✓ | 限定的 |
| ファイルをまたいだ参照を検索 | ✓ | — |
| シンボルの名前変更 | ✓ | — |
| Python サポート | ✓ | — |
| オフライン動作（CLI なし） | — | ✓ |

&nbsp;

&nbsp;
