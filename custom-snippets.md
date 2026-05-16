# <a name="custom-snippets"></a>Starter Custom Snippets

Spck Editor's [Custom Snippets](./editor-lite#custom-snippets) feature lets you define reusable code templates that show up in the autocomplete list. This page provides ready-to-paste starter packs for the most common patterns across popular frameworks — so you can skip writing the boilerplate yourself.

Each pack is a JSON config keyed by language mode (`javascript_ls` for the frontend frameworks, `python_ls` for the Python ones, `html_ls`/`css_ls` for template and style fragments). Pick a framework, hit **Copy**, and paste into `Settings > Editor > Custom Snippets > Import`.

## <a name="how-to-use"></a>How to Use

1. Pick a framework below and click **Copy JSON**.
2. In Spck Editor, open `Settings > Editor > Custom Snippets`.
3. Tap the menu and choose **Import** (or paste into a new snippet file for that language).
4. The snippets will appear in your editor's autocomplete list as you type their trigger name.

All snippets use tab-stop placeholders (`$1`, `$2`, `$0`) so the cursor jumps between editable positions after insertion. See the [Custom Snippets reference](./editor-lite#custom-snippets) for the placeholder syntax.

## <a name="snippet-packs"></a>Snippet Packs

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), functional and arrow components, custom hooks, forwardRef, and Context Provider patterns.</p>
    <p>Target mode: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Download react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router scaffolding (page, layout, loading, error, not-found), route handlers, server actions, generateMetadata/StaticParams, Link, Image, dynamic import, navigation hooks, and middleware.</p>
    <p>Target mode: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Download nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API primitives, lifecycle hooks, defineProps/Emits, Pinia store, and Options API fallback (script side) plus SFC scaffolding, v-for/v-if/v-model/v-bind/v-on, slots, transitions, and router-link (template side).</p>
    <p>Target modes: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Download vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Reactive declarations, lifecycle, all store types, and event dispatcher (script side) plus component scaffold, {#if}/{#each}/{#await}/{#key} blocks, bind:/on:/class:/use: directives, store subscription, and slots (template side).</p>
    <p>Target modes: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Download svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Common utility groupings (flex/grid layouts, cards, buttons, inputs, badges, alerts), responsive and dark-mode variants, plus CSS-side @apply/@layer/@tailwind directives.</p>
    <p>Target modes: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Download tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>App scaffold, all HTTP methods, async route with try/catch, middleware, auth middleware, error handler, Router module, CORS, static files, and request param helpers.</p>
    <p>Target mode: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Download express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>App scaffolding, GET/POST/PUT/DELETE routes, async handlers, path and query params, Pydantic models, Depends, HTTPException, APIRouter, BackgroundTasks, CORS middleware, file uploads, and lifespan handlers.</p>
    <p>Target mode: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Download fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copy JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Models, function and class-based views, DRF APIView/ViewSet/Serializer, forms, urlpatterns, admin registration, migrations, custom managers, signals, and management commands.</p>
    <p>Target mode: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Download django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Copy JSON</button>
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

## <a name="customizing"></a>Customizing the Snippets

These packs are starting points — most teams add their own patterns over time. Useful additions to consider:

- **Component scaffolds** matching your project's file structure (e.g. a `page` snippet that includes your standard imports and layout wrapper).
- **Test boilerplate** — your testing framework's `describe`/`it` structure with the imports you always need.
- **Logging or telemetry** calls with your project-specific event names pre-filled.
- **API client calls** — wrap your standard `fetch` / axios / SDK call pattern with error handling.

The JSON format is straightforward — each snippet is just a `name` (what shows in autocomplete) and a `snippet` body. Edit the downloaded JSON in any text editor before importing.

## <a name="see-also"></a>See Also

- [Custom Snippets reference](./editor-lite#custom-snippets) — placeholder syntax, scoping, and how to manage snippets in-app.
- [Getting Started](./editor) — installation and an overview of Spck Editor features.
