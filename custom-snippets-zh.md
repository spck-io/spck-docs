# <a name="custom-snippets"></a>自定义代码片段入门包

Spck Editor 的[自定义代码片段](./editor-lite#custom-snippets)功能允许你定义可复用的代码模板，这些模板会显示在自动补全列表中。本页面为主流框架中最常见的模式提供了即粘即用的入门包——让你无需自己编写样板代码。

每个包都是一个以语言模式为键的 JSON 配置（前端框架使用 `javascript_ls`，Python 框架使用 `python_ls`，模板和样式片段使用 `html_ls`/`css_ls`）。选择一个框架，点击**复制**，然后粘贴到 `设置 > 编辑器 > 自定义代码片段 > 导入`。

## <a name="how-to-use"></a>使用方法

1. 在下方选择一个框架，点击**复制 JSON**。
2. 在 Spck Editor 中，打开 `设置 > 编辑器 > 自定义代码片段`。
3. 点击菜单并选择**导入**（或粘贴到该语言的新片段文件中）。
4. 输入触发器名称后，片段将出现在编辑器的自动补全列表中。

![在 Spck Editor 中导入自定义代码片段包](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

所有片段均使用制表位占位符（`$1`、`$2`、`$0`），插入后光标会在可编辑位置之间跳转。占位符语法详见[自定义代码片段参考](./editor-lite#custom-snippets)。

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
    <p>Hook（useState、useEffect、useRef、useMemo、useCallback、useContext、useReducer）、函数式和箭头函数组件、自定义 Hook、forwardRef 和 Context Provider 模式。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>下载 react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router 脚手架（page、layout、loading、error、not-found）、路由处理器、服务端 Action、generateMetadata/StaticParams、Link、Image、动态导入、导航 Hook 和中间件。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>下载 nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 基础元素、生命周期钩子、defineProps/Emits、Pinia store、Options API 回退（脚本侧），以及 SFC 脚手架、v-for/v-if/v-model/v-bind/v-on、插槽、过渡动画和 router-link（模板侧）。</p>
    <p>目标模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>下载 vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>响应式声明、生命周期、所有 store 类型和事件分发器（脚本侧），以及组件脚手架、{#if}/{#each}/{#await}/{#key} 块、bind:/on:/class:/use: 指令、store 订阅和插槽（模板侧）。</p>
    <p>目标模式：<code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>下载 svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>常用工具类分组（flex/grid 布局、卡片、按钮、输入框、徽标、警告提示）、响应式和暗色模式变体，以及 CSS 侧的 @apply/@layer/@tailwind 指令。</p>
    <p>目标模式：<code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>下载 tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>应用脚手架、所有 HTTP 方法、带 try/catch 的异步路由、中间件、认证中间件、错误处理器、Router 模块、CORS、静态文件和请求参数助手。</p>
    <p>目标模式：<code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>下载 express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>应用脚手架、GET/POST/PUT/DELETE 路由、异步处理器、路径和查询参数、Pydantic 模型、Depends、HTTPException、APIRouter、BackgroundTasks、CORS 中间件、文件上传和生命周期处理器。</p>
    <p>目标模式：<code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>下载 fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">复制 JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>模型、基于函数和类的视图、DRF APIView/ViewSet/Serializer、表单、urlpatterns、管理后台注册、迁移、自定义管理器、信号和管理命令。</p>
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

## <a name="customizing"></a>自定义片段

这些包只是起点——大多数团队会随着时间积累自己的模式。你可以直接在应用内编辑任何片段：

![在 Spck Editor 中编辑自定义代码片段](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

值得考虑添加的内容：

- **组件脚手架**，与你项目的文件结构相匹配（例如，包含标准导入和布局包裹器的 `page` 片段）。
- **测试样板** — 测试框架的 `describe`/`it` 结构，以及你总会需要的导入。
- **日志或遥测调用**，预填你项目特定的事件名称。
- **API 客户端调用** — 将你标准的 `fetch`/axios/SDK 调用模式封装上错误处理。

JSON 格式简单明了——每个片段只有一个 `name`（显示在自动补全中的名称）和一个 `snippet` 正文。导入前在任意文本编辑器中编辑下载的 JSON 即可。

## <a name="see-also"></a>另请参阅

- [自定义代码片段参考](./editor-lite#custom-snippets) — 占位符语法、作用域及应用内片段管理方式。
- [入门指南](./editor) — Spck Editor 的安装与功能概述。
