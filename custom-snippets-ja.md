# <a name="custom-snippets"></a>カスタムスニペット

Spck Editor の[カスタムスニペット](./editor-lite#custom-snippets)機能を使うと、オートコンプリート一覧に表示される再利用可能なコードテンプレートを定義できます。このページでは、人気のフレームワークでよく使われるパターン向けに、貼り付けるだけで使えるスターターパックを提供しています。これでボイラープレートコードを自分で書く手間を省けます。

> **提供範囲:** カスタムスニペットはプレミアム機能です。Spck Editor の完全版では [Gold サブスクリプション](https://spck.io/pricing)で解除でき、[Spck Editor Lite](./editor-lite) の買い切り版でも利用できます。

各パックは言語モードごとにキー分けされた JSON 設定です（フロントエンド系フレームワークには `javascript_ls`、Python 系には `python_ls`、テンプレート／スタイル断片には `html_ls`/`css_ls`）。フレームワークを選び、**JSON をコピー** を押して、Spck Editor のスニペット設定エディタに貼り付けてください。

## <a name="how-to-use"></a>使い方

1. 以下からフレームワークを選び、**JSON をコピー** をクリックします。
2. Spck Editor で `Settings > Editor > Custom Snippets` を開きます。
3. スニペットリスト上部の **Code** アイコンをタップして、設定を JSON として編集します。
4. コピーした JSON を貼り付け、**Update** をタップしてスニペット設定を上書きします。
5. トリガー名を入力すると、エディタのオートコンプリート一覧にスニペットが表示されます。

![Spck Editor でカスタムスニペットパックをインポートする](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

すべてのスニペットは Tab ストップのプレースホルダー（`$1`、`$2`、`$0`）を使用しているため、挿入後にカーソルが編集可能な位置を順に移動します。プレースホルダー構文については[カスタムスニペットリファレンス](./editor-lite#custom-snippets)を参照してください。

## <a name="snippet-packs"></a>スニペットパック

<div class="snippet-tabs">
  <div class="snippet-tabs-nav">
    <button type="button" class="snippet-tab-btn" data-pack="react">React</button>
    <button type="button" class="snippet-tab-btn" data-pack="nextjs">Next.js</button>
    <button type="button" class="snippet-tab-btn" data-pack="vue">Vue</button>
    <button type="button" class="snippet-tab-btn" data-pack="svelte">Svelte</button>
    <button type="button" class="snippet-tab-btn" data-pack="tailwind">Tailwind</button>
    <button type="button" class="snippet-tab-btn" data-pack="express">Express</button>
    <button type="button" class="snippet-tab-btn" data-pack="fastapi">FastAPI</button>
    <button type="button" class="snippet-tab-btn" data-pack="django">Django</button>
  </div>

  <div class="snippet-tab-pane" data-pack="react">
    <p>Hooks（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、関数コンポーネントとアロー関数コンポーネント、カスタムフック、forwardRef、Context Provider パターン。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>react.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router の雛形（page、layout、loading、error、not-found）、ルートハンドラー、Server Actions、generateMetadata/StaticParams、Link、Image、動的 import、ナビゲーションフック、ミドルウェア。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API のプリミティブ、ライフサイクルフック、defineProps/Emits、Pinia ストア、Options API のフォールバック（スクリプト側）に加え、SFC の雛形、v-for/v-if/v-model/v-bind/v-on、スロット、トランジション、router-link（テンプレート側）。</p>
    <p>対象モード: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>リアクティブ宣言、ライフサイクル、すべてのストア型、イベントディスパッチャー（スクリプト側）に加え、コンポーネントの雛形、{#if}/{#each}/{#await}/{#key} ブロック、bind:/on:/class:/use: ディレクティブ、ストアの購読、スロット（テンプレート側）。</p>
    <p>対象モード: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>よく使うユーティリティの組み合わせ（flex/grid レイアウト、カード、ボタン、入力欄、バッジ、アラート）、レスポンシブおよびダークモードのバリアント、CSS 側の @apply/@layer/@tailwind ディレクティブ。</p>
    <p>対象モード: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>アプリの雛形、すべての HTTP メソッド、try/catch を使った async ルート、ミドルウェア、認証ミドルウェア、エラーハンドラー、Router モジュール、CORS、静的ファイル、リクエストパラメータ用のヘルパー。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>アプリの雛形、GET/POST/PUT/DELETE ルート、非同期ハンドラー、パスとクエリのパラメータ、Pydantic モデル、Depends、HTTPException、APIRouter、BackgroundTasks、CORS ミドルウェア、ファイルアップロード、lifespan ハンドラー。</p>
    <p>対象モード: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>モデル、関数ベースおよびクラスベースのビュー、DRF APIView/ViewSet/Serializer、フォーム、urlpatterns、admin 登録、マイグレーション、カスタムマネージャー、シグナル、management コマンド。</p>
    <p>対象モード: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>django.json をダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">JSON をコピー</button>
      <pre><code class="hljs" id="snippet-json-django"></code></pre>
    </div>
  </div>
</div>

<script>
(function () {
  var loaded = {};

  function escapeHtml(s) {
    return s.replace(/&/g, '&amp;').replace(/</g, '&lt;').replace(/>/g, '&gt;');
  }

  function loadPack(id) {
    if (loaded[id]) return Promise.resolve(loaded[id]);
    return fetch('/assets/snippets/' + id + '.json')
      .then(function (r) { return r.text(); })
      .then(function (text) {
        loaded[id] = text;
        var el = document.getElementById('snippet-json-' + id);
        if (el) el.innerHTML = escapeHtml(text);
        return text;
      })
      .catch(function () {
        var el = document.getElementById('snippet-json-' + id);
        if (el) el.textContent = 'Failed to load snippet pack.';
      });
  }

  function activate(id) {
    document.querySelectorAll('.snippet-tab-btn').forEach(function (b) {
      b.classList.toggle('active', b.dataset.pack === id);
    });
    document.querySelectorAll('.snippet-tab-pane').forEach(function (p) {
      p.classList.toggle('active', p.dataset.pack === id);
    });
    loadPack(id);
  }

  document.querySelectorAll('.snippet-tab-btn').forEach(function (btn) {
    btn.addEventListener('click', function () { activate(btn.dataset.pack); });
  });

  document.querySelectorAll('.snippet-copy-btn').forEach(function (btn) {
    btn.addEventListener('click', function () {
      var targetId = btn.dataset.target;
      var packId = targetId.replace('snippet-json-', '');
      loadPack(packId).then(function (text) {
        if (!text) return;
        var done = function () {
          var original = btn.textContent;
          btn.textContent = 'Copied!';
          btn.classList.add('copied');
          setTimeout(function () {
            btn.textContent = original;
            btn.classList.remove('copied');
          }, 1500);
        };
        if (navigator.clipboard && navigator.clipboard.writeText) {
          navigator.clipboard.writeText(text).then(done, done);
        } else {
          var ta = document.createElement('textarea');
          ta.value = text;
          document.body.appendChild(ta);
          ta.select();
          try { document.execCommand('copy'); } catch (_) {}
          document.body.removeChild(ta);
          done();
        }
      });
    });
  });

  activate('react');
})();
</script>

## <a name="customizing"></a>スニペットのカスタマイズ

これらのパックはあくまで出発点です。多くの開発者は時間をかけて独自のパターンを追加していきます。アプリ内で各スニペットを直接編集できます。

![Spck Editor でカスタムスニペットを編集する](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

追加すると便利なものの例:

- **コンポーネントの雛形** — プロジェクトのファイル構成に合わせたもの（例: 標準的な import とレイアウトラッパーを含む `page` スニペット）。
- **テスト用ボイラープレート** — 必ず必要となる import を含めた、テストフレームワークの `describe`/`it` 構造。
- **ロギングやテレメトリ**呼び出し — プロジェクト固有のイベント名を事前に埋め込んだもの。
- **API クライアント呼び出し** — エラーハンドリングを含めた、標準的な `fetch` / axios / SDK 呼び出しパターンのラッパー。

JSON のフォーマットは単純で、各スニペットはオートコンプリートに表示される `name` とスニペット本体 `snippet` だけで構成されます。ダウンロードした JSON を任意のテキストエディタで編集してから、スニペット設定に貼り付けてください。

## <a name="see-also"></a>関連項目

- [カスタムスニペットリファレンス](./editor-lite#custom-snippets) — プレースホルダー構文、スコープ、アプリ内でのスニペット管理方法。
- [Spck Editor Lite](./editor-lite) — カスタムスニペットを含む買い切り版。
- [料金](https://spck.io/pricing) — Spck Editor 完全版向けの Gold サブスクリプションの詳細。
- [はじめに](./editor) — インストールと Spck Editor の機能の概要。
