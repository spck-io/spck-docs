# <a name="custom-snippets"></a>Стартовые пользовательские сниппеты

Функция [Пользовательские сниппеты](./editor-lite#custom-snippets) в Spck Editor позволяет определять многоразовые шаблоны кода, которые появляются в списке автодополнения. На этой странице представлены готовые стартовые наборы для самых распространённых паттернов в популярных фреймворках — чтобы вам не приходилось писать шаблонный код самостоятельно.

Каждый набор — это JSON-конфигурация, организованная по языковому режиму (`javascript_ls` для фронтенд-фреймворков, `python_ls` для Python, `html_ls`/`css_ls` для шаблонов и стилей). Выберите фреймворк, нажмите **Копировать** и вставьте в `Настройки > Редактор > Пользовательские сниппеты > Импорт`.

## <a name="how-to-use"></a>Как использовать

1. Выберите фреймворк ниже и нажмите **Копировать JSON**.
2. В Spck Editor откройте `Настройки > Редактор > Пользовательские сниппеты`.
3. Нажмите на меню и выберите **Импорт** (или вставьте в новый файл сниппетов для этого языка).
4. Сниппеты появятся в списке автодополнения редактора при вводе их имени-триггера.

![Импорт набора пользовательских сниппетов в Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Все сниппеты используют заполнители с табуляцией (`$1`, `$2`, `$0`), поэтому курсор перемещается между редактируемыми позициями после вставки. Синтаксис заполнителей описан в [справочнике по пользовательским сниппетам](./editor-lite#custom-snippets).

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
    <p>Хуки (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), функциональные и стрелочные компоненты, пользовательские хуки, forwardRef и паттерны Context Provider.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Скачать react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Скаффолдинг App Router (page, layout, loading, error, not-found), обработчики маршрутов, серверные действия, generateMetadata/StaticParams, Link, Image, динамический импорт, хуки навигации и middleware.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Скачать nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Примитивы Composition API, хуки жизненного цикла, defineProps/Emits, хранилище Pinia и запасной вариант Options API (сторона скрипта), а также скаффолдинг SFC, v-for/v-if/v-model/v-bind/v-on, слоты, переходы и router-link (сторона шаблона).</p>
    <p>Целевые режимы: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Скачать vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Реактивные объявления, жизненный цикл, все типы хранилищ и диспетчер событий (сторона скрипта), а также скаффолдинг компонента, блоки {#if}/{#each}/{#await}/{#key}, директивы bind:/on:/class:/use:, подписка на хранилище и слоты (сторона шаблона).</p>
    <p>Целевые режимы: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Скачать svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Распространённые группы утилит (макеты flex/grid, карточки, кнопки, поля ввода, бейджи, алерты), адаптивные варианты и варианты тёмного режима, плюс CSS-директивы @apply/@layer/@tailwind.</p>
    <p>Целевые режимы: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Скачать tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Скаффолдинг приложения, все HTTP-методы, асинхронный маршрут с try/catch, middleware, middleware аутентификации, обработчик ошибок, модуль Router, CORS, статические файлы и хелперы параметров запроса.</p>
    <p>Целевой режим: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Скачать express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Скаффолдинг приложения, маршруты GET/POST/PUT/DELETE, асинхронные обработчики, параметры пути и запроса, модели Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, CORS middleware, загрузка файлов и обработчики жизненного цикла.</p>
    <p>Целевой режим: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Скачать fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Копировать JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Модели, представления на основе функций и классов, DRF APIView/ViewSet/Serializer, формы, urlpatterns, регистрация в админке, миграции, пользовательские менеджеры, сигналы и команды управления.</p>
    <p>Целевой режим: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Скачать django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Копировать JSON</button>
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

Эти наборы — лишь отправная точка. Большинство команд со временем добавляют собственные паттерны. Любой сниппет можно редактировать прямо в приложении:

![Редактирование пользовательского сниппета в Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Полезные дополнения для рассмотрения:

- **Скаффолдинг компонентов**, соответствующий структуре файлов вашего проекта (например, сниппет `page` со стандартными импортами и обёрткой макета).
- **Шаблонный код тестов** — структура `describe`/`it` вашего тестового фреймворка с нужными импортами.
- **Вызовы логирования или телеметрии** с предзаполненными именами событий, специфичных для проекта.
- **Вызовы API-клиента** — оберните стандартный паттерн вызова `fetch`/axios/SDK с обработкой ошибок.

Формат JSON прост — каждый сниппет состоит только из `name` (то, что отображается в автодополнении) и тела `snippet`. Перед импортом отредактируйте скачанный JSON в любом текстовом редакторе.

## <a name="see-also"></a>Смотрите также

- [Справочник по пользовательским сниппетам](./editor-lite#custom-snippets) — синтаксис заполнителей, область видимости и управление сниппетами в приложении.
- [Начало работы](./editor) — установка и обзор возможностей Spck Editor.
