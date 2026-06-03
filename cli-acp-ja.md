# <a name="ai-coding-agents-acp"></a>モバイルでのAIコーディングエージェント（ACP）

**Claude Code**、**OpenAI Codex**、または **Gemini CLI** を、Spck Editor の **AI Chat** を通してスマートフォンから直接実行できます。Spck CLI は、オープンな [Agent Client Protocol (ACP)](https://agentclientprotocol.com/) を介して、エディタとローカルにインストールされたエージェント CLI を橋渡しします。モデルはあなたのマシンで、あなたのサブスクリプションを使って、実際のファイルに対して実行され、モバイル端末から監視できます。

![Spck Editor の AI Chat における ACP ローカル AI モード。スマートフォンからデスクトップ上の Claude Code を操作している様子](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>ACP とは何か、なぜ使うのか

Agent Client Protocol (ACP) は Zed Industries による、エディタと AI エージェント間の通信のためのオープン標準で、Language Server Protocol (LSP) と同じ思想に基づいています。Spck CLI 0.6.0+ は ACP を実装しており、Spck Editor の AI Chat（クライアント）とインストール済みの ACP 対応エージェントバイナリ（エージェント）の間の**トランスポート**として機能します。

アプリ内のサーバー経由 AI Chat と比較して、ローカル ACP の経路では次の利点があります:

- **あなた自身のサブスクリプション** — エージェント呼び出しは Claude Code / ChatGPT / Gemini のアカウントに課金され、Spck Editor の AI クォータは消費しません。
- **実際のファイルシステムアクセス** — エージェントは CLI を通してディスク上の実ファイルを読み書きします。エディタのインメモリコピーではありません。
- **ネイティブツール** — ファイルウォッチャー、言語サーバー、シェルコマンドはあなたの実マシン上で動作します。
- **デスクトップとの継続性** — デスクで使っているのと同じ `claude` / `gemini` / `codex` ログインがモバイルチャットを駆動します。

## <a name="acp-supported-agents"></a>サポートされる AI エージェント

利用したいエージェントをインストールしてください。Spck CLI が起動時に自動検出します。

| エージェント       | インストール                                                                         |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>インストールとセットアップ

### 1. Spck CLI をインストール

まだ持っていない場合:

```bash
npm install -g spck
# またはインストールせずに実行
npx spck
```

完全な初回セットアップウィザードについては [Spck CLI を始める](./cli-start) を参照してください。

### 2. 1つ以上のエージェント CLI をインストール

使いたいエージェントを選びます。複数インストールしてもよく — AI Chat はセッションごとに切り替えさせてくれます。インストールコマンドは上の [サポートされる AI エージェント](#acp-supported-agents) の表を参照してください。

### 3. 各エージェントを一度認証する

エージェント CLI はそれぞれ Spck Editor の外で独自のログインを管理します:

```bash
claude            # Anthropic Claude Code のログインフロー
codex login       # OpenAI Codex のログインフロー（codex-acp が使用）
gemini            # Google Gemini のログインフロー
```

このステップをスキップすると、Spck Editor は最初にチャットを開始したときに `ACP agent requires authentication; run <binary> login and retry` のようなエラーを表示します。

### 4. Spck CLI を起動

```bash
cd /path/to/your/project
spck
```

起動時、CLI は利用可能なエージェントを列挙したエージェントごとの検出レポートを出力し、続いてメインの機能ブロックに `✅ ACP agents: Claude Code, Gemini CLI` のような 1 行のサマリーを表示します。何も利用できない場合は、代わりにサーバー経由の AI Chat にフォールバックします。

### 5. Spck Editor を接続

QR コードをスキャンするか [手動入力](./cli-start#connecting) を使用します。接続後、Spck Editor で **AI Chat** を開くと、トランスポート切替にローカルエージェントがクラウドオプションと並んで表示されます。

## <a name="acp-authentication"></a>認証

各エージェントは Spck CLI が動作するマシン上で独自の認証情報を管理します。エージェントごとに一度ログインフローを実行してください:

```bash
# Claude Code
claude

# Codex（codex-acp は Codex CLI 独自のログインをラップ）
codex login

# Gemini CLI
gemini
```

再インストールやマシン移動時は、新しいホストでログインをやり直してください。認証は **ホストごと、エージェントごと** に行われます — Spck Editor 自体はこれらの認証情報を保持しません。

## <a name="acp-billing"></a>課金とレート制限

ACP はあなたのマシン上で、あなた自身の認証情報を使ってエージェントを実行するため、**すべての使用量はそのプロバイダーのアカウントに課金されます** — Spck Editor のサブスクリプションには課金されません。このモードでは Spck Editor と Spck リレーサーバーは純粋なトランスポートとして動作し、ACP のトラフィックに対してアプリ内 AI クォータを一切消費しません。

### Claude Code の課金

> ⚠️ **重要 — Claude Code はサードパーティ製ツールから駆動されるとき、別のレート制限バケットを適用します。**
>
> Claude Code がサードパーティクライアントから ACP 経由で呼び出されると、Anthropic はそのトラフィックを Pro / Max サブスクリプションでの対話的な `claude` CLI セッションとは**別のレート制限バケット**にカウントします。実際上の影響: 対話的な Claude Code の余裕が残っているのにサードパーティバケットを使い切る（あるいはその逆）ことがあり、両者を合算することはできません。
>
> 現在の消費量を確認するには `claude` 内の `/usage` と [Anthropic Console](https://platform.claude.com/usage) を、お使いのプランに該当する数値については [Claude Code のコスト・制限ドキュメント](https://code.claude.com/docs/en/costs) を参照してください。

### Codex (codex-acp) の課金

OpenAI Codex CLI 自身の認証経由で課金されます — あなたの OpenAI API キーまたは ChatGPT ログインです。使用量はそのアカウントが持つどのプランに対してもカウントされます。料金とクォータは対話的な `codex` の使用と同じです。現在の数値については [openai.com/codex](https://github.com/openai/codex) と OpenAI ダッシュボードを参照してください。

### Gemini CLI の課金

Google アカウントまたは Gemini API キー経由で課金されます。使用量はそのログインに紐づく Gemini プランまたは API クォータに対してカウントされます。レート制限の詳細は [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits) を参照してください。

## <a name="acp-configuration"></a>設定

ACP はデフォルトで有効で、プロジェクトの `spck-cli.config.json` で設定します:

```json
{
  "acp": {
    "enabled": true
  }
}
```

完全なスキーマは [設定 → ACP 設定](./cli-config#acp-settings) を参照してください。

### プロジェクト単位で ACP を無効化

このホストで Spck Editor がローカルエージェントを駆動できないようにしたい場合:

```json
{
  "acp": {
    "enabled": false
  }
}
```

無効化されると、エディタのトランスポート切替はローカルエージェントオプションを非表示にし、`acp.*` の RPC はすべて `FEATURE_DISABLED` で拒否されます。セットアップウィザードは初回起動時にこの質問をします（デフォルト `Y`）。このオプション以前の設定は `acp.enabled: true` を自動的に追加して再保存されます。

### 単一のエージェントを無効化

他のエージェントで ACP を有効にしたまま _特定の_ エージェントが提供されないようにするには、そのエージェントのバイナリをアンインストールします。検出は CLI 起動のたびに実行されるため、エディタのトランスポート切替はそれをリストから除外します。

## <a name="acp-vs-server-routed"></a>ローカル ACP とサーバー経由 AI Chat の比較

| 機能                                       | サーバー経由（デフォルト、CLI なし） | ローカル（ACP、CLI 接続済み）            |
| ------------------------------------------ | ----------------------------------- | --------------------------------------- |
| モデルの実行場所                            | Spck クラウド                       | あなたのマシン                          |
| 認証情報                                   | あなたの Spck Editor アカウント     | エージェント自身のログイン / API キー   |
| ファイルアクセス                            | エディタのインメモリファイルシステム | CLI ルート経由でディスク上の実ファイル  |
| Spck Editor の AI クォータを消費するか      | はい                                | **いいえ** — エージェントプロバイダーに課金 |
| CLI を起動せずに動作するか                  | はい                                | いいえ（CLI + WebSocket が必要）        |
| 利用可能なエージェント                      | Spck がホストするモデル             | Claude Code, Codex, Gemini CLI          |
| ツール使用権限プロンプトの携帯表示          | 該当する場合                        | はい、ACP 経由で転送                    |
| トークンのストリーミング                    | はい                                | はい                                    |
| マルチターンチャット                        | はい                                | はい                                    |

プロジェクトの途中でもトランスポートを切り替えられます — AI Chat は CLI の接続状態と検出されたエージェントに応じて、現在利用可能な経路を表示します。

## <a name="acp-tmux"></a>長時間セッションのための Tmux との組み合わせ

ACP セッションはエディタの再接続をまたいで生き続けますが、Spck CLI プロセス自体はそのターミナルが閉じると終了します。大規模なリファクタリングや数時間にわたる計画セッションなどの長時間エージェント作業では、SSH の切断、ターミナルの終了、ノート PC のスリープを乗り越えるために [tmux](./tmux) セッション内で CLI を起動します:

```bash
tmux new -s spck
spck
# Ctrl+B のあと D でデタッチ
```

スマートフォンからも Spck CLI のターミナル経由で再接続し、`tmux attach -t spck` でエージェントをライブ監視できます。永続的なバックグラウンドサービスとして CLI を実行する方法を含む完全なパターンについては [Tmux の使用](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile) を参照してください。

Linux ホストの場合、[Claude Skill: Linux Service](./claude-skill) ページに、Spck CLI を `systemd` サービスとして実行するためのワンコマンド・セットアップがあり、WebSocket — およびその上の ACP セッション — が起動時に自動的に立ち上がります。

## <a name="acp-faq"></a>よくある質問

### スマートフォンで Claude Code を使えますか？

はい。デスクトップに Claude Code をインストールし、`claude` で認証してから、プロジェクトで `spck` を実行します。スマートフォンから Spck Editor を接続し、AI Chat のトランスポート切替で Claude Code を選びます。モデルはあなたのサブスクリプションを使ってデスクトップで動作し、スマートフォンから操作します。

### Spck Editor は私の Claude / OpenAI / Gemini の API キーを見ますか？

いいえ。各エージェント CLI は Spck CLI が動作するマシン上で独自の認証情報を管理します。ACP メッセージはスマートフォンと CLI の間の暗号化された WebSocket でトンネルされますが、エージェント自身の認証トークンがあなたのホストを離れることはありません。

### Spck Editor を介して Claude Code を使う追加コストはありますか？

Spck Editor からの追加料金はありません。エージェントの使用量は、デスクで対話的にエージェントを実行しているのとまったく同じように、あなたの Anthropic / OpenAI / Google プランに対してカウントされます — ただし、Anthropic はサードパーティクライアントに別のレート制限バケットを適用します。上記の [課金とレート制限](#acp-billing) を参照してください。

### ACP を使うには Spck Editor の有料サブスクリプションが必要ですか？

いいえ。無料枠（CLI 接続 1 日 30 分）でも任意の ACP エージェントを操作できます。Spck Editor の AI クォータを消費するのはアプリ内のサーバー経由 AI Chat のみです。

### チャットの途中で Wi-Fi 接続が切れたらどうなりますか？

エージェントプロセスは CLI ホスト上で生き続けます。エディタが再接続すると、セッションは完全なチャット履歴とともに再開されます。オフライン中に到着したストリーミング出力は再接続時に再生されます。

### ラップトップではなくリモートサーバーでエージェントを動かせますか？

はい。Spck CLI は到達可能な任意の Linux/macOS ホスト — 開発 VM、自宅サーバー、ワークステーション — で動作させ、リレーサーバー経由で接続できます。接続の合間にも CLI を生かしておくには [tmux](./tmux) または [systemd スキル](./claude-skill) と組み合わせてください。

### ACP は Spck Editor Lite で動作しますか？

はい。ACP のトラフィックは Spck Editor Lite がサポートするファイルシステムや git と同じ WebSocket トランスポートを使用します。CLI 設定で `security.userAuthenticationEnabled` を `false` にしてください — Firebase 認証は Lite ではサポートされません。[設定 → ユーザー認証](./cli-config#user-authentication) を参照してください。

### AI Chat にエージェントが表示されないのはなぜですか？

CLI 起動ログのエージェントごとの行を確認してください:

- エージェントが検出されない — インストールしてください（[サポートされる AI エージェント](#acp-supported-agents) を参照）。
- 検出されているがエディタに表示されない — エージェント自身のログインフロー（`claude`、`codex login`、`gemini`）を完了したか確認してください。
- ACP が無効 — `.spck-editor/config/spck-cli.config.json` の `acp.enabled` を確認してください。[設定](./cli-config#acp-settings) を参照。

## <a name="acp-troubleshooting"></a>トラブルシューティング

### エージェントは検出されたがセッションが開始しない

ほとんどの場合、エージェントが認証されていないことを意味します。CLI ホストでエージェントのログインフローを実行してください:

```bash
claude              # その後ブラウザ認証を完了
codex login
gemini
```

それでも問題が続く場合は、`.spck-editor/logs/` の CLI のログでエージェントの stderr 出力を確認してください。通常は失敗している認証またはバイナリを指し示しています。

### チャット中にレート制限エラーが発生する

Claude Code の場合、エディタは Anthropic の 429 をそのまま表示します。[Anthropic Console の使用量ページ](https://platform.claude.com/usage) と [Claude Code のコストドキュメント](https://code.claude.com/docs/en/costs) を確認してください — サードパーティのレート制限バケットは対話的な `claude` の枠とは別であることを忘れないでください。

Codex と Gemini については、エディタはプロバイダー自身のクォータエラーをそのまま表示します。プロバイダーのコンソールから解決してください。

### ACP セッション開始時に CLI がクラッシュする

Spck CLI は ACP トラフィックを `.spck-editor/logs/` にログします。問題を再現しながら最新のログファイルを追跡してください:

```bash
tail -f .spck-editor/logs/spck-*.log
```

[github.com/spck-editor](https://github.com/spck-editor) で関連するスニペットを添えてバグを報告してください。

### エージェントがプロジェクトルートの外を変更する

ACP エージェントは CLI で設定された `root` ディレクトリにスコープされます。その外への書き込みが見られる場合は issue を報告してください — これは起こるべきではありません。回避策として、`spck --root /path/to/specific/project` を実行してスコープをさらに狭めてください。

## <a name="acp-see-also"></a>関連項目

- [Spck CLI を始める](./cli-start) — 初回のインストール、認証、接続
- [CLI リファレンス](./cli) — リレーサーバー、日々のワークフロー、接続制限
- [設定 → ACP 設定](./cli-config#acp-settings) — `acp.enabled` 設定オプション
- [高度な使い方](./cli-advanced) — CLI フラグ、複数プロジェクト、モバイルプロンプトのヒント
- [Tmux の使用](./tmux) — 再接続をまたいで ACP セッションを生かす
- [Claude Skill: Linux Service](./claude-skill) — Spck CLI を `systemd` サービスとして実行し、ACP を常時利用可能にする
- [Agent Client Protocol 仕様](https://agentclientprotocol.com/) — ACP が実装するオープン標準
- [Claude Code ドキュメント](https://docs.claude.com/en/docs/claude-code/overview)
- [Gemini CLI リポジトリ](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
