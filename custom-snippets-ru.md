# <a name="custom-snippets"></a>Пользовательские сниппеты

Функция [Пользовательские сниппеты](./editor-lite#custom-snippets) в Spck Editor позволяет определять переиспользуемые шаблоны кода, которые отображаются в списке автодополнения. На этой странице представлены готовые к вставке стартовые наборы для самых распространённых шаблонов популярных фреймворков — чтобы вам не приходилось писать шаблонный код самостоятельно.

> **Доступность:** Пользовательские сниппеты — это премиум-функция. Она открывается по [подписке Gold](https://spck.io/pricing) в полной версии Spck Editor или через разовую покупку [Spck Editor Lite](./editor-lite).

Каждый набор — это JSON-конфигурация, сгруппированная по языковому режиму (`javascript_ls` для фронтенд-фреймворков, `python_ls` для Python, `html_ls`/`css_ls` для фрагментов шаблонов и стилей). Выберите фреймворк, нажмите **Скопировать JSON** и вставьте в редактор конфигурации сниппетов в Spck Editor.

## <a name="how-to-use"></a>Как использовать

1. Выберите фреймворк ниже и нажмите **Скопировать JSON**.
2. В Spck Editor откройте `Settings > Editor > Custom Snippets`.
3. Нажмите на значок **Code** (в верхней части списка сниппетов), чтобы отредактировать конфигурацию как JSON.
4. Вставьте скопированный JSON и нажмите **Update**, чтобы перезаписать конфигурацию сниппетов.
5. Сниппеты появятся в списке автодополнения вашего редактора, как только вы начнёте вводить имя их триггера.

![Импорт набора пользовательских сниппетов в Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Все сниппеты используют табуляционные плейсхолдеры (`$1`, `$2`, `$0`), поэтому курсор переходит между редактируемыми позициями после вставки. Синтаксис плейсхолдеров см. в [справочнике по Пользовательским сниппетам](./editor-lite#custom-snippets).

## <a name="snippet-packs"></a>Наборы сниппетов

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
    <p>Хуки (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), функциональные и стрелочные компоненты, пользовательские хуки, forwardRef и шаблоны Context Provider.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Скачать react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Каркас App Router (page, layout, loading, error, not-found), обработчики маршрутов, server actions, generateMetadata/StaticParams, Link, Image, динамический import, хуки навигации и middleware.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Скачать nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Примитивы Composition API, хуки жизненного цикла, defineProps/Emits, хранилище Pinia и резервный вариант Options API (со стороны script), а также каркас SFC, v-for/v-if/v-model/v-bind/v-on, слоты, переходы и router-link (со стороны шаблона).</p>
    <p>Целевые режимы: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Скачать vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Реактивные объявления, жизненный цикл, все типы хранилищ и event dispatcher (со стороны script), а также каркас компонента, блоки {#if}/{#each}/{#await}/{#key}, директивы bind:/on:/class:/use:, подписка на хранилище и слоты (со стороны шаблона).</p>
    <p>Целевые режимы: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Скачать svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Распространённые группы утилит (раскладки flex/grid, карточки, кнопки, поля ввода, бейджи, уведомления), варианты для адаптивной вёрстки и тёмной темы, а также CSS-директивы @apply/@layer/@tailwind.</p>
    <p>Целевые режимы: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Скачать tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Каркас приложения, все HTTP-методы, асинхронный маршрут с try/catch, middleware, middleware аутентификации, обработчик ошибок, модуль Router, CORS, статические файлы и хелперы для параметров запроса.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Скачать express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Каркас приложения, маршруты GET/POST/PUT/DELETE, асинхронные обработчики, path- и query-параметры, модели Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, загрузка файлов и обработчики lifespan.</p>
    <p>Целевой режим: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Скачать fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Скопировать JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Модели, представления на основе функций и классов, DRF APIView/ViewSet/Serializer, формы, urlpatterns, регистрация в admin, миграции, пользовательские менеджеры, сигналы и management-команды.</p>
    <p>Целевой режим: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Скачать django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Скопировать JSON</button>
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

## <a name="customizing"></a>Настройка сниппетов

Эти наборы — лишь отправная точка: большинство разработчиков со временем добавляют свои собственные шаблоны. Любой сниппет можно отредактировать прямо в приложении:

![Редактирование пользовательского сниппета в Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Полезные дополнения, которые стоит рассмотреть:

- **Каркасы компонентов**, соответствующие структуре файлов вашего проекта (например, сниппет `page`, включающий стандартные импорты и обёртку макета).
- **Шаблоны тестов** — структура `describe`/`it` вашего тестового фреймворка с импортами, которые всегда нужны.
- Вызовы **логирования или телеметрии** с предзаполненными именами событий, специфичными для вашего проекта.
- **Вызовы API-клиента** — оберните ваш стандартный шаблон вызова `fetch` / axios / SDK обработкой ошибок.

Формат JSON прост: каждый сниппет — это просто `name` (то, что отображается в автодополнении) и тело `snippet`. Отредактируйте скачанный JSON в любом текстовом редакторе перед вставкой в конфигурацию сниппетов.

## <a name="see-also"></a>См. также

- [Справочник по Пользовательским сниппетам](./editor-lite#custom-snippets) — синтаксис плейсхолдеров, область действия и управление сниппетами в приложении.
- [Spck Editor Lite](./editor-lite) — версия с разовой покупкой, включающая Пользовательские сниппеты.
- [Цены](https://spck.io/pricing) — подробности о подписке Gold для полной версии Spck Editor.
- [Начало работы](./editor) — установка и обзор возможностей Spck Editor.
