# <a name="claude-skill"></a>Claude スキル：Spck CLI を Linux サービスとして実行する

このページでは、Spck CLI（`spck`）を Linux の `systemd` サービスとしてインストールする作業を自動化する[Claude Code スキル](https://docs.claude.com/en/docs/claude-code/skills)をダウンロードできます。スキルをインストールすると、Claude Code に「spck をサービスとして実行して」と依頼するだけで、環境を確認し、絶対パスを含む正しいユニットファイルを生成してインストールし、正常に動作していることを確認してくれます — チェックリストからコマンドをコピーする必要はありません。

このスキルは[Tmux を使う → 代替手段: Linux サービス](./tmux#linux-service)で説明されているのと同じ systemd 設定を、手動でユニットファイルを書く際に見落としがちな事前チェックと失敗診断も含めて自動化します。

## <a name="download"></a>ダウンロード

スキルファイルをダウンロードして、ローカルの Claude Code スキルディレクトリに保存します:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

または手動でダウンロード: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — `~/.claude/skills/spck-cli-service/SKILL.md` に配置してください。

## <a name="what-the-skill-does"></a>スキルの動作

呼び出されると、スキルは Claude Code を全インストール手順を通じてガイドします:

1. ホストが `systemd` を実行している Linux であることを確認します。
2. `spck` への絶対パスを解決します（`ExecStart` を壊す `PATH` の不一致を回避）。
3. `node` が `nvm` 経由でインストールされている場合に警告します — それらのパスは Node アップグレードのたびに変わり、サービスを暗黙的に壊します。
4. `~/.spck-editor/.credentials.json` が存在することを確認します（CLI はサービスとして実行する前に少なくとも一度対話的に実行されている必要があります）。
5. ニーズに応じて**ユーザーサービス**（`systemctl --user`、`sudo` 不要）と**システムサービス**のどちらかを選択します。
6. 実際のパスを埋めたユニットファイルを書き込みます — プレースホルダーなし。
7. `daemon-reload`、`enable --now` を実行し、CLI がリレーサーバーに接続したことを確認するためにジャーナルを追跡します。

スキルは最も一般的な7つの失敗モード（誤った `ExecStart` パス、認証情報の欠如、プロジェクトディレクトリのパーミッションエラー、`start-limit-hit` に達したリスタートループ、npm アップグレード後の古くなった nvm パスなど）も文書化しているため、Claude Code はユニットファイルを再生成するだけでなく、壊れたサービスを診断できます。

## <a name="installation"></a>インストール

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**手順1 — スキルファイルをダウンロードする:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**手順2 — Claude Code が認識したことを確認する:**

```bash
claude /skills
```

リストに `spck-cli-service` が表示されるはずです。表示されない場合は、Claude Code を再起動してスキルディレクトリを再スキャンさせてください。

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop は macOS と Linux で同じ `~/.claude/skills/` ディレクトリからスキルを読み込みます。Windows ではパスは `%USERPROFILE%\.claude\skills\` ですが、スキル自体は Linux ホストでのみ動作するため、Claude Desktop を実行しているマシンではなく、`spck` を実行したいマシンにインストールしてください。

リモート Linux サーバーを管理している場合は、そのサーバー上で SSH 経由で Claude Code を実行してください（またはサーバーへの完全なシェルアクセスを提供する Spck CLI ターミナル経由で）。ローカルの Mac にスキルをインストールしても、リモート Linux サービスの設定には役立ちません。

</div>
  </div>
</div>

## <a name="usage"></a>使い方

インストール後、自然言語で Claude Code に依頼することでスキルを呼び出せます。スキルを起動する例:

- 「spck を systemd サービスとしてインストールして」
- 「Spck CLI を起動時に自動起動させて」
- 「spck-cli.service が再起動し続けているんだけど、デバッグできる?」
- 「SSH が切れても生き残るように spck をデーモンとして実行して」

Claude Code はスキルを読み込み、事前チェックを実行し（各コマンドの承認を求めます）、ユニットファイルを生成してインストールします。各コマンドを承認前に確認してください — 特に `sudo` で `/etc/systemd/system/` に書き込むコマンドは注意が必要です。

## <a name="what-gets-installed"></a>インストールされるもの

スキルは単一のユニットファイルをインストールします。ユーザーサービスの場合:

```bash
~/.config/systemd/user/spck-cli.service
```

内容は次のようになります:

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

システムサービスの場合、ファイルは `/etc/systemd/system/spck-cli.service` に置かれ、`User=` と `Group=` ディレクティブが追加されます。スキルは環境に基づいて適切なバリアントを選択し、実際の絶対パスをファイルに書き込みます。

## <a name="why-a-skill-instead-of-copy-paste"></a>コピーペーストではなくスキルを使う理由

[tmux ドキュメント](./tmux#linux-service)のユニットファイルは出発点ですが、サービスが実際に動作するためにはいくつかの点が正確でなければなりません:

- `ExecStart` は `spck` への**絶対パス**でなければなりません。ログインシェル内の `which spck` は `.bashrc` からの PATH 操作を解決しますが、systemd はそれを見ません。
- `spck` が `nvm` 配下にインストールされている場合、パスに Node のバージョンが埋め込まれます — Node をアップグレードすると次の再起動まで暗黙的にサービスが壊れます。
- `~/.spck-editor/.credentials.json` を作成するために、CLI は少なくとも一度対話的に実行されている必要があります。認証情報なしでサービスが新規起動すると、明白なエラーなくクリーンに終了します。
- `User=` は `WorkingDirectory` を所有している必要があります。そうでないとファイル監視が `EACCES` に当たり、CLI がリスタートループに入ります。
- ユーザーサービスはヘッドレスサーバーで `loginctl enable-linger` が必要です。そうでなければ、ログインセッションがアクティブな間だけ実行されます。

スキルはこれらすべてを自動化するため、覚える必要がありません。

## <a name="uninstall"></a>アンインストール

サービスを無効化して削除します:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

システムサービスの場合:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Claude Code からスキル自体を削除するには:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>関連項目

- [Tmux を使う](./tmux) — SSH 切断時に CLI を維持するための `tmux` を使った代替アプローチ。
- [高度な使い方](./cli-advanced) — CLI コマンドの完全なリファレンス、設定の上書き、マルチプロジェクト設定。
- [設定](./cli-config) — ユニットファイルがカバーしないターミナル、ファイルシステム、セキュリティ、認証の設定。
