# <a name="git-support"></a>Git 対応

Spck は Android・iOS のローカルプロジェクト、ブラウザー、Spck CLI 経由のリモートプロジェクトで Git に対応しています。このガイドでは、プロバイダーの認証情報、プルリクエスト、コミットの確認、競合解決、各環境の制限を説明します。

基本的な Git 連携、コミット履歴、マージ競合の解決は無料版で利用できます。[拡張 Git 連携](#enhanced-git-integration)ではプルリクエスト管理とコミット内のファイル差分が追加されます。

## <a name="git-credentials"></a>Git 認証情報とプルリクエスト

**Git menu → Git Credentials** を開き、プロバイダーを選択してアクセストークンを保存します。以下の作成・ヘルプリンクは新しいタブで開くため、Spck に戻ってトークンを貼り付けられます。

| プロバイダー | トークンの設定 | Git とプルリクエストの権限 |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">GitHub トークンを作成</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">設定ガイド</a> | リポジトリを選択します。作成リンクでは **Contents: Read and write**、**Pull requests: Read and write**、**Metadata: Read** が事前選択されます。 |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">GitLab トークンを作成</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">設定ガイド</a> | 作成リンクではマージリクエスト用の `api` スコープが事前選択されます。 |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">API トークンを作成</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">設定ガイド</a> | **Create API token with scopes**、**Bitbucket** を選択し、`read:repository:bitbucket`、`write:repository:bitbucket`、`read:pullrequest:bitbucket`、`write:pullrequest:bitbucket` を手動で指定します。API 認証には Atlassian アカウントのメールアドレスを使用します。 |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">PAT 作成ガイド</a> | 組織の **User settings → Personal access tokens → New Token** を開き、組織を選び、**Code (Read & write)** を手動で指定します。 |

プルリクエストを作成するには、ソースブランチをコミットしてプッシュし、**Git menu → Create PR** を開きます。リモートと認証情報を選び、異なるターゲットブランチ、タイトル、説明を指定します。**Generate with AI** はブランチの共通祖先からのコミット済み変更をもとに下書きを作成できます。先にターゲットブランチをフェッチしてください。下書きを確認してから **Create PR** を選択します。GitLab ではマージリクエストが作成されます。

プルリクエストの作成・管理は[拡張 Git 連携](#enhanced-git-integration)に含まれる **Premium 機能**です。Lite ではアプリの買い切り購入に含まれます。フル版では有効な Supporter・Gold・Node サブスクリプション、または Spck for NodeJS ターミナルの永久利用権を持つアカウントでログインしてください。

## <a name="pull-request-management"></a>プルリクエスト管理（Premium）

エディター内でプルリクエストを管理できます。対応するリモートは **GitHub.com、GitLab.com、Bitbucket Cloud、Azure DevOps** です。GitLab ではマージリクエストと呼びます。

1. Git プロジェクトを開き、上記の権限を持つプロバイダーのトークンを **Git menu → Git Credentials** に追加します。
2. **Git menu → Pull Requests** を開き、リモートと認証情報を選んで未完了のリクエストを表示します。
3. リクエストを選択すると、タイトル、説明、作成者、ソース・ターゲットブランチ、状態を確認できます。
4. 変更されたファイルを選び、読み取り専用の差分を確認してからマージを判断します。
5. マージ可能なリクエストは **Merge**、マージせず閉じる場合は **Close** を選択します。必須レビュー、チェック、トークン権限、ブランチルールは引き続き適用されます。下書きや競合のあるリクエストはこのダイアログからマージできません。

プロバイダー側で変更があった場合は **Refresh** で一覧を更新します。リクエスト詳細には、レビューやチェックなどを行うためのプロバイダーへのリンクもあります。

新規作成は上記の **Git menu → Create PR** を使用します。ソースブランチのプッシュが必要な場合は、作成前に **Push** が表示されます。任意の AI 下書き機能は設定済みの AI サービスとその利用制限を使用し、Lite に含まれるプルリクエスト利用権とは別です。

トークン権限が原因で作成に失敗した場合は、プロバイダーのリンクからトークンを作成・更新し、**Git Credentials** に保存して再試行してください。PR の下書きは保持されます。

## <a name="enhanced-git-integration"></a>拡張 Git 連携

拡張 Git 連携では、変更の確認と共有のための次の機能が追加されます。

- **プルリクエスト管理：** 作成、未完了リクエストの閲覧、変更ファイルと差分の確認、マージ、クローズができます。設定と手順は[プルリクエスト管理](#pull-request-management)をご覧ください。
- **コミットの確認：** 作業中のファイルを変更せずに、コミット内の変更ファイルと差分を確認できます。

Git パネルの **History** を開き、コミットを選択すると追加・変更・削除されたファイルが表示されます。ファイルを選ぶと最初の親コミットに対する読み取り専用差分が開きます。最初のコミットは空のツリーと比較します。コミット済みの内容を使用するため、未コミットの編集は差分に影響しません。バイナリファイルはテキスト差分として表示できません。

履歴項目を長押し、または右クリックして **View Commit** を選択することもできます。

拡張 Git 連携は次に含まれます。

- **Spck Editor Lite：** アプリの買い切り購入で永久に利用でき、ログインは不要です。
- **Spck for NodeJS ターミナルの永久利用購入：** 購入したアカウントで永久に利用でき、ログインが必要です。
- **Supporter・Gold・Node サブスクリプション：** 契約期間中に利用でき、ログインが必要です。

基本的な Git 連携とコミット履歴は無料版でも引き続き利用できます。プランの詳細は[料金](https://spck.io/pricing)をご覧ください。

## <a name="merge-conflict-resolution"></a>マージ競合を解決する

差分ビューアーでは作業ファイルの競合も解決できます。基本的な Git 連携の一部で、Premium は不要です。

1. Git の変更一覧から競合中のファイルを開きます。
2. 各競合で **Accept Current**、**Accept Incoming**、**Accept Both** を選択します。ファイルを編集して手動で変更を組み合わせることもできます。
3. 結果を確認し、競合マーカーをすべて削除したら、差分ビューアーの **Resolve** を選択して解決済みファイルをステージします。
4. 残りのファイルを解決してからマージをコミットします。

タッチ端末では、ファイルや Git 項目を長押しするとコンテキストメニューが開きます。Git の状態文字はファイル名の色を補い、変更を判別しやすくします。

## <a name="git-limitations"></a>Git の制限

### <a name="git-limitations-overview"></a>概要

Git の実装は、プロジェクトの保存場所と使用する Spck のバージョンによって異なります。

| 環境 | Git の実装 | 主な制約 |
| --- | --- | --- |
| Android・iOS アプリ（Lite、Spck for NodeJS を含む） | ローカルプロジェクト用にネイティブコンパイルされた **libgit2** | 端末ストレージ上のプロジェクトが必要です。端末のリソースとファイルシステムの制約は引き続き適用されます。 |
| ブラウザー・埋め込みエディター | JavaScript の [isomorphic-git](https://isomorphic-git.org/) | ブラウザーのメモリ、ストレージ、ネットワークの制約が適用されます。 |
| Spck CLI 経由のリモートプロジェクト | ホストの **Git バイナリ** | ホストのリソース、ファイルシステム、認証情報、インストール済み Git を使用します。 |

現在のモバイル版は、ブラウザーの Git エンジンではなくネイティブ Git を使用します。ローカル操作で **Native Git requires a device folder** と表示されたら、プロジェクトを端末ストレージに移動してください。エディターのブラウザーデータベース内にしかないプロジェクトは、モバイルのネイティブ Git クライアントを使用できません。

プルリクエスト管理は **Git Credentials** に保存したトークンでプロバイダー API を直接呼び出します。ブラウザーのログイン Cookie は使わず、API 応答もキャッシュしないため、更新時に最新のリクエスト状態とブランチ情報を取得できます。権限は [Git 認証情報とプルリクエスト](#git-credentials)、対応プロバイダーと操作は[プルリクエスト管理](#pull-request-management)をご覧ください。

### <a name="git-limitations-memory"></a>メモリの制約

- Android・iOS のネイティブ Git は JavaScript の Git エンジン外で処理します。ブラウザーエンジンのメモリ制約は、モバイル Git の固定上限ではありません。
- ネイティブ Git も空きメモリとディスク容量を必要とします。大きなリポジトリや pack ファイルは端末のリソースを超え、操作の失敗や OS によるアプリ終了の原因になる場合があります。
- ブラウザーの Git は JavaScript メモリとストレージの制限を受けます。大きな pack ファイルの処理では大量のメモリが必要になり、クローンやフェッチに失敗する場合があります。

> 💡 **ヒント：** 大きなリポジトリでは、可能なら浅いクローンを使用するか、リポジトリの小さな部分を扱ってください。

### <a name="git-limitations-symlinks"></a>シンボリックリンクの互換性

- ブラウザーストレージとエディターの端末ファイルシステム層では、シンボリックリンクを含むリポジトリに**エミュレートされたリンク**を使用します。
- モバイル Git が libgit2 に変わっても、ファイルシステムの制限はなくならず、OS の実際のシンボリックリンクも保証されません。
- 実際のリンクと実行時のリンク先解決を前提とするビルドツール、パッケージマネージャー、スクリプトでは、エミュレートされたリンクの動作が異なる場合があります。
- 実際のシンボリックリンクが必要なら、対応するファイルシステムと権限を持つホストのリモートプロジェクトを使用してください。

### <a name="git-limitations-cli"></a>代替手段として CLI を使う

大きなリポジトリやホストのファイルシステム・Git ツールが必要な作業では、**Spck CLI 経由のリモートプロジェクト**を使用してください。Spck で編集しながら、**ホストの Git バイナリ**で Git 操作を実行できます。

- リポジトリ操作にはモバイル端末やブラウザーではなくホストのメモリとディスクを使用します。
- シンボリックリンクはホスト OS のファイルシステム対応と権限に従います。
- エディターの Git コントロールにないコマンドは、ホストの Git ツールで実行してください。

ホストの接続は [Spck CLI のはじめ方](./cli-start)をご覧ください。リモートプロジェクトには Spck アカウントが必要で、プランのアクセス制限が適用されます。Lite のサブスクリプション要件は[リモートプロジェクト](./editor-lite#remote-projects)をご覧ください。端末ストレージへのクローンには引き続きモバイルアプリのネイティブ Git クライアントを使用します。

## <a name="git-related-guides"></a>関連ガイド

- [スクリーンリーダー対応（試験的）](./screen-reader-support)：アクセシブルな移動、ソース管理コントロール、フィードバック。
- [Spck Editor Lite](./editor-lite#enhanced-git-integration)：買い切り購入に含まれる Git ツール。
- [Spck CLI のはじめ方](./cli-start)：リモートプロジェクトを接続し、ホストの Git ツールを使用する。
