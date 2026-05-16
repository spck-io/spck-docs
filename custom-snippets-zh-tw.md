# <a name="custom-snippets"></a>自訂程式碼片段入門包

Spck Editor 的[自訂程式碼片段](./editor-lite#custom-snippets)功能讓你能定義可重複使用的程式碼範本，這些範本會顯示在自動補全清單中。本頁面為主流框架中最常見的模式提供了即貼即用的入門包——讓你無需自行編寫樣板程式碼。

每個包都是以語言模式為鍵的 JSON 設定（前端框架使用 `javascript_ls`，Python 框架使用 `python_ls`，範本和樣式片段使用 `html_ls`/`css_ls`）。選擇一個框架，點擊**複製**，然後貼到 `設定 > 編輯器 > 自訂程式碼片段 > 匯入`。

## <a name="how-to-use"></a>使用方式

1. 在下方選擇一個框架，點擊**複製 JSON**。
2. 在 Spck Editor 中，開啟 `設定 > 編輯器 > 自訂程式碼片段`。
3. 點選選單並選擇**匯入**（或貼到該語言的新片段檔案中）。
4. 輸入觸發器名稱後，片段將出現在編輯器的自動補全清單中。

![在 Spck Editor 中匯入自訂程式碼片段包](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

所有片段均使用定位停駐點占位符（`$1`、`$2`、`$0`），插入後游標會在可編輯位置之間跳轉。占位符語法詳見[自訂程式碼片段參考](./editor-lite#custom-snippets)。

## <a name="snippet-packs"></a>片段包

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
    <p>Hook（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、函數式與箭頭函數元件、自訂 Hook、forwardRef 和 Context Provider 模式。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>下載 react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router 鷹架（page、layout、loading、error、not-found）、路由處理器、伺服器 Action、generateMetadata/StaticParams、Link、Image、動態匯入、導覽 Hook 和中介軟體。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>下載 nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 基礎元素、生命週期鉤子、defineProps/Emits、Pinia store、Options API 後備（腳本側），以及 SFC 鷹架、v-for/v-if/v-model/v-bind/v-on、插槽、過渡動畫和 router-link（模板側）。</p>
    <p>目標模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>下載 vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>響應式宣告、生命週期、所有 store 類型和事件分發器（腳本側），以及元件鷹架、{#if}/{#each}/{#await}/{#key} 區塊、bind:/on:/class:/use: 指令、store 訂閱和插槽（模板側）。</p>
    <p>目標模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>下載 svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>常用工具類分組（flex/grid 版面配置、卡片、按鈕、輸入框、徽標、警告提示）、響應式和深色模式變體，以及 CSS 側的 @apply/@layer/@tailwind 指令。</p>
    <p>目標模式：<code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>下載 tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>應用鷹架、所有 HTTP 方法、帶 try/catch 的非同步路由、中介軟體、認證中介軟體、錯誤處理器、Router 模組、CORS、靜態檔案和請求參數助手。</p>
    <p>目標模式：<code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>下載 express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>應用鷹架、GET/POST/PUT/DELETE 路由、非同步處理器、路徑和查詢參數、Pydantic 模型、Depends、HTTPException、APIRouter、BackgroundTasks、CORS 中介軟體、檔案上傳和生命週期處理器。</p>
    <p>目標模式：<code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>下載 fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">複製 JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>模型、基於函數和類別的視圖、DRF APIView/ViewSet/Serializer、表單、urlpatterns、管理後台注冊、遷移、自訂管理器、信號和管理命令。</p>
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

## <a name="customizing"></a>自訂片段

這些包只是起點——大多數團隊會隨時間累積自己的模式。你可以直接在應用程式內編輯任何片段：

![在 Spck Editor 中編輯自訂程式碼片段](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

值得考慮新增的內容：

- **元件鷹架**，符合你專案的檔案結構（例如，包含標準匯入和版面配置包裝器的 `page` 片段）。
- **測試樣板** — 測試框架的 `describe`/`it` 結構，以及你總是需要的匯入。
- **日誌或遙測呼叫**，預填你專案特定的事件名稱。
- **API 用戶端呼叫** — 將你標準的 `fetch`/axios/SDK 呼叫模式封裝上錯誤處理。

JSON 格式簡單明瞭——每個片段只有一個 `name`（顯示在自動補全中的名稱）和一個 `snippet` 正文。匯入前在任意文字編輯器中編輯下載的 JSON 即可。

## <a name="see-also"></a>另請參閱

- [自訂程式碼片段參考](./editor-lite#custom-snippets) — 占位符語法、作用域及應用程式內片段管理方式。
- [入門指南](./editor) — Spck Editor 的安裝與功能概述。
