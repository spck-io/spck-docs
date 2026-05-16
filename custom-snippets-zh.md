# <a name="custom-snippets"></a>自定义代码片段

Spck Editor 的[自定义代码片段](./editor-lite#custom-snippets)功能让你可以定义可重用的代码模板，它们会出现在自动补全列表中。本页面提供了可直接粘贴使用的入门套件，涵盖热门框架中最常见的模式——这样你就不用自己再写那些样板代码了。

> **可用性：** 自定义代码片段是一项高级功能。在 Spck Editor 完整版中，可通过 [Gold 订阅](https://spck.io/pricing)解锁；也可通过一次性购买 [Spck Editor Lite](./editor-lite) 获得。

每个套件都是按语言模式（前端框架用 `javascript_ls`，Python 框架用 `python_ls`，模板和样式片段用 `html_ls`/`css_ls`）组织的 JSON 配置。选择一个框架，点击 **复制 JSON**，然后粘贴到 Spck Editor 的代码片段配置编辑器中。

## <a name="how-to-use"></a>使用方法

1. 在下方选择一个框架，点击 **复制 JSON**。
2. 在 Spck Editor 中打开 `Settings > Editor > Custom Snippets`。
3. 点击代码片段列表顶部的 **Code** 图标，以 JSON 形式编辑配置。
4. 粘贴复制的 JSON，然后点击 **Update** 覆盖你的代码片段配置。
5. 输入触发名称时，代码片段会出现在编辑器的自动补全列表中。

![在 Spck Editor 中导入自定义代码片段套件](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

所有代码片段都使用制表符占位符（`$1`、`$2`、`$0`），插入后光标会在可编辑位置之间跳转。占位符语法请参阅[自定义代码片段参考](./editor-lite#custom-snippets)。

## <a name="snippet-packs"></a>代码片段套件

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
    <p>Hooks（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、函数式与箭头组件、自定义 hook、forwardRef 以及 Context Provider 模式。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>下载 react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router 脚手架（page、layout、loading、error、not-found）、路由处理程序、server actions、generateMetadata/StaticParams、Link、Image、动态 import、导航 hook 以及中间件。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>下载 nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 基础原语、生命周期 hook、defineProps/Emits、Pinia store 以及 Options API 备选方案（script 端）；外加 SFC 脚手架、v-for/v-if/v-model/v-bind/v-on、插槽、过渡和 router-link（模板端）。</p>
    <p>目标模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>下载 vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>响应式声明、生命周期、所有 store 类型以及事件分发器（script 端）；外加组件脚手架、{#if}/{#each}/{#await}/{#key} 块、bind:/on:/class:/use: 指令、store 订阅和插槽（模板端）。</p>
    <p>目标模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>下载 svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>常用工具类组合（flex/grid 布局、卡片、按钮、输入框、徽章、提示）、响应式与深色模式变体，以及 CSS 端 @apply/@layer/@tailwind 指令。</p>
    <p>目标模式：<code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>下载 tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>应用脚手架、所有 HTTP 方法、带 try/catch 的异步路由、中间件、鉴权中间件、错误处理器、Router 模块、CORS、静态文件以及请求参数辅助方法。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>下载 express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>应用脚手架、GET/POST/PUT/DELETE 路由、异步处理器、path 和 query 参数、Pydantic 模型、Depends、HTTPException、APIRouter、BackgroundTasks、CORS 中间件、文件上传以及 lifespan 处理器。</p>
    <p>目标模式：<code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>下载 fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>模型、基于函数和基于类的视图、DRF APIView/ViewSet/Serializer、表单、urlpatterns、admin 注册、迁移、自定义 manager、signals 以及 management 命令。</p>
    <p>目标模式：<code>python_ls</code> · <a href="/assets/snippets/django.json" download>下载 django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">复制 JSON</button>
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

## <a name="customizing"></a>自定义代码片段

这些套件只是起点——大多数开发者会随着时间推移添加自己的模式。你可以直接在应用内编辑任何代码片段：

![在 Spck Editor 中编辑自定义代码片段](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

一些值得考虑的实用补充：

- **组件骨架**，与你项目的文件结构相匹配（例如包含标准导入和布局包装器的 `page` 代码片段）。
- **测试样板** ——你测试框架的 `describe`/`it` 结构，加上你总是会用到的那些导入。
- **日志或遥测**调用，预先填好项目特定的事件名称。
- **API 客户端调用** ——把你标准的 `fetch` / axios / SDK 调用模式连同错误处理一起封装好。

JSON 格式很简单——每个代码片段只包含一个 `name`（自动补全中显示的内容）和一个 `snippet` 主体。在粘贴到代码片段配置之前，可以在任何文本编辑器中编辑下载的 JSON。

## <a name="see-also"></a>另请参阅

- [自定义代码片段参考](./editor-lite#custom-snippets) ——占位符语法、作用域以及在应用内管理代码片段的方法。
- [Spck Editor Lite](./editor-lite) ——包含自定义代码片段的一次性购买版本。
- [价格](https://spck.io/pricing) —— Spck Editor 完整版的 Gold 订阅详情。
- [入门](./editor) —— Spck Editor 的安装和功能概览。
