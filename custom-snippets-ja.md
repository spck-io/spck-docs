# <a name="custom-snippets"></a>カスタムスニペット スターターパック

Spck Editorの[カスタムスニペット](./editor-lite#custom-snippets)機能を使うと、オートコンプリートリストに表示される再利用可能なコードテンプレートを定義できます。このページでは、主要なフレームワークでよく使われるパターンに対応したすぐに使えるスターターパックを提供しています。ボイラープレートを自分で書く手間が省けます。

各パックは言語モードをキーとするJSON設定です（フロントエンドフレームワークには`javascript_ls`、Pythonには`python_ls`、テンプレートとスタイルには`html_ls`/`css_ls`）。フレームワークを選択し、**コピー**をクリックして、`設定 > エディタ > カスタムスニペット > インポート`に貼り付けてください。

## <a name="how-to-use"></a>使い方

1. 下からフレームワークを選び、**JSONをコピー**をクリックします。
2. Spck Editorで`設定 > エディタ > カスタムスニペット`を開きます。
3. メニューをタップして**インポート**を選択します（またはその言語用の新しいスニペットファイルに貼り付けます）。
4. スニペットはトリガー名を入力するとエディタのオートコンプリートリストに表示されます。

![Spck Editorでカスタムスニペットパックをインポートする](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

すべてのスニペットはタブストッププレースホルダー（`$1`、`$2`、`$0`）を使用しているため、挿入後にカーソルが編集可能な位置間を移動します。プレースホルダーの構文については[カスタムスニペットリファレンス](./editor-lite#custom-snippets)を参照してください。

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
    <p>フック（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、関数コンポーネントとアロー関数コンポーネント、カスタムフック、forwardRef、Context Providerパターン。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>react.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Routerのスキャフォールド（page、layout、loading、error、not-found）、ルートハンドラー、サーバーアクション、generateMetadata/StaticParams、Link、Image、動的インポート、ナビゲーションフック、ミドルウェア。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition APIのプリミティブ、ライフサイクルフック、defineProps/Emits、Piniaストア、Options APIフォールバック（スクリプト側）に加え、SFCスキャフォールド、v-for/v-if/v-model/v-bind/v-on、スロット、トランジション、router-link（テンプレート側）。</p>
    <p>対象モード: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>リアクティブな宣言、ライフサイクル、すべてのストアタイプ、イベントディスパッチャー（スクリプト側）に加え、コンポーネントのスキャフォールド、{#if}/{#each}/{#await}/{#key}ブロック、bind:/on:/class:/use:ディレクティブ、ストアサブスクリプション、スロット（テンプレート側）。</p>
    <p>対象モード: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>一般的なユーティリティグループ（フレックス/グリッドレイアウト、カード、ボタン、入力フィールド、バッジ、アラート）、レスポンシブおよびダークモードのバリアント、CSSサイドの@apply/@layer/@tailwindディレクティブ。</p>
    <p>対象モード: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>アプリのスキャフォールド、すべてのHTTPメソッド、try/catch付きの非同期ルート、ミドルウェア、認証ミドルウェア、エラーハンドラー、Routerモジュール、CORS、静的ファイル、リクエストパラメーターヘルパー。</p>
    <p>対象モード: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>アプリのスキャフォールド、GET/POST/PUT/DELETEルート、非同期ハンドラー、パスパラメーターとクエリパラメーター、Pydanticモデル、Depends、HTTPException、APIRouter、BackgroundTasks、CORSミドルウェア、ファイルアップロード、ライフスパンハンドラー。</p>
    <p>対象モード: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSONをコピー</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>モデル、関数ベースおよびクラスベースのビュー、DRF APIView/ViewSet/Serializer、フォーム、urlpatterns、管理者登録、マイグレーション、カスタムマネージャー、シグナル、管理コマンド。</p>
    <p>対象モード: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>django.jsonをダウンロード</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">JSONをコピー</button>
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

これらのパックはあくまで出発点です。多くのチームは時間をかけて独自のパターンを追加していきます。アプリ内で直接スニペットを編集することもできます:

![Spck Editorでカスタムスニペットを編集する](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

追加を検討すると便利なもの:

- プロジェクトのファイル構造に合わせた**コンポーネントのスキャフォールド**（例: 標準インポートとレイアウトラッパーを含む`page`スニペット）。
- **テストのボイラープレート** — テストフレームワークの`describe`/`it`構造と常に必要なインポート。
- プロジェクト固有のイベント名が入力済みの**ロギングやテレメトリの呼び出し**。
- エラー処理付きの標準的な`fetch`/axios/SDK呼び出しパターンをラップした**APIクライアント呼び出し**。

JSONフォーマットはシンプルです — 各スニペットは`name`（オートコンプリートに表示されるもの）と`snippet`本体だけです。ダウンロードしたJSONをインポート前に任意のテキストエディタで編集してください。

## <a name="see-also"></a>関連項目

- [カスタムスニペットリファレンス](./editor-lite#custom-snippets) — プレースホルダーの構文、スコープ、アプリ内でのスニペット管理。
- [はじめに](./editor) — Spck Editorのインストールと機能概要。
