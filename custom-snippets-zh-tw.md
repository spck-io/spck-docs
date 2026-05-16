# <a name="custom-snippets"></a>自訂程式碼片段

Spck Editor 的[自訂程式碼片段](./editor-lite#custom-snippets)功能讓你可以定義可重複使用的程式碼範本，它們會出現在自動完成清單中。本頁提供可直接貼上使用的入門套件，涵蓋熱門框架中最常見的模式——讓你不必自己撰寫樣板程式碼。

> **可用性：** 自訂程式碼片段是進階功能。在 Spck Editor 完整版中，可透過 [Gold 訂閱](https://spck.io/pricing)解鎖；也可以透過一次性購買 [Spck Editor Lite](./editor-lite) 取得。

每個套件都是依照語言模式（前端框架使用 `javascript_ls`，Python 框架使用 `python_ls`，範本與樣式片段使用 `html_ls`/`css_ls`）整理的 JSON 設定。選擇一個框架，按 **複製 JSON**，然後貼到 Spck Editor 的程式碼片段設定編輯器中。

## <a name="how-to-use"></a>使用方法

1. 在下方選擇一個框架，按一下 **複製 JSON**。
2. 在 Spck Editor 中開啟 `Settings > Editor > Custom Snippets`。
3. 點選程式碼片段清單頂端的 **Code** 圖示，以 JSON 形式編輯設定。
4. 貼上複製的 JSON，然後點選 **Update** 覆寫程式碼片段設定。
5. 當你輸入觸發名稱時，程式碼片段就會出現在編輯器的自動完成清單中。

![在 Spck Editor 中匯入自訂程式碼片段套件](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

所有程式碼片段都使用定位點佔位符（`$1`、`$2`、`$0`），插入後游標會在可編輯位置之間跳動。佔位符語法請參考[自訂程式碼片段參考](./editor-lite#custom-snippets)。

## <a name="snippet-packs"></a>程式碼片段套件

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
    <p>Hooks（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、函式型與箭頭函式元件、自訂 hooks、forwardRef，以及 Context Provider 模式。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>下載 react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router 樣板（page、layout、loading、error、not-found）、路由處理器、server actions、generateMetadata/StaticParams、Link、Image、動態 import、導覽 hooks 以及中介軟體。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>下載 nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 基本元素、生命週期 hooks、defineProps/Emits、Pinia store，以及 Options API 備援（script 端）；外加 SFC 樣板、v-for/v-if/v-model/v-bind/v-on、插槽、轉場與 router-link（範本端）。</p>
    <p>目標模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>下載 vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>反應式宣告、生命週期、所有 store 類型以及事件分派器（script 端）；外加元件樣板、{#if}/{#each}/{#await}/{#key} 區塊、bind:/on:/class:/use: 指令、store 訂閱與插槽（範本端）。</p>
    <p>目標模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>下載 svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>常用工具類組合（flex/grid 版面配置、卡片、按鈕、輸入框、徽章、警示）、響應式與深色模式變體，以及 CSS 端 @apply/@layer/@tailwind 指令。</p>
    <p>目標模式：<code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>下載 tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>應用程式樣板、所有 HTTP 方法、附 try/catch 的非同步路由、中介軟體、驗證中介軟體、錯誤處理器、Router 模組、CORS、靜態檔案，以及請求參數輔助函式。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>下載 express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>應用程式樣板、GET/POST/PUT/DELETE 路由、非同步處理器、path 與 query 參數、Pydantic 模型、Depends、HTTPException、APIRouter、BackgroundTasks、CORS 中介軟體、檔案上傳以及 lifespan 處理器。</p>
    <p>目標模式：<code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>下載 fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>模型、函式型與類別型視圖、DRF APIView/ViewSet/Serializer、表單、urlpatterns、admin 註冊、遷移、自訂 manager、signals 以及 management 命令。</p>
    <p>目標模式：<code>python_ls</code> · <a href="/assets/snippets/django.json" download>下載 django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">複製 JSON</button>
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

## <a name="customizing"></a>自訂程式碼片段

這些套件只是起點——大多數開發者會隨著時間加入自己的模式。你可以直接在應用程式內編輯任何程式碼片段：

![在 Spck Editor 中編輯自訂程式碼片段](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

值得考慮加入的實用內容：

- **元件樣板**，配合你專案的檔案結構（例如包含標準匯入與版面配置包裝的 `page` 程式碼片段）。
- **測試樣板** ——你測試框架的 `describe`/`it` 結構，加上你總是會用到的匯入。
- **記錄或遙測**呼叫，預先填好你專案特有的事件名稱。
- **API 客戶端呼叫** ——把你標準的 `fetch` / axios / SDK 呼叫模式連同錯誤處理一起包裝好。

JSON 格式很單純——每個程式碼片段只包含一個 `name`（出現在自動完成中）和一個 `snippet` 主體。在貼到程式碼片段設定之前，可以在任何文字編輯器中編輯下載的 JSON。

## <a name="see-also"></a>另請參閱

- [自訂程式碼片段參考](./editor-lite#custom-snippets) ——佔位符語法、作用範圍，以及在應用程式內管理程式碼片段的方法。
- [Spck Editor Lite](./editor-lite) ——包含自訂程式碼片段的一次性購買版本。
- [價格](https://spck.io/pricing) —— Spck Editor 完整版的 Gold 訂閱詳情。
- [快速開始](./editor) —— Spck Editor 的安裝及功能概覽。
