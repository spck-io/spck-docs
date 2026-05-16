# <a name="custom-snippets"></a>Snippets personalizados de inicio rápido

La función [Snippets personalizados](./editor-lite#custom-snippets) de Spck Editor te permite definir plantillas de código reutilizables que aparecen en la lista de autocompletado. Esta página proporciona paquetes de inicio listos para pegar con los patrones más comunes en los frameworks populares — para que no tengas que escribir el código repetitivo tú mismo.

Cada paquete es una configuración JSON organizada por modo de lenguaje (`javascript_ls` para los frameworks frontend, `python_ls` para los de Python, `html_ls`/`css_ls` para fragmentos de plantillas y estilos). Elige un framework, haz clic en **Copiar** y pégalo en `Ajustes > Editor > Snippets personalizados > Importar`.

## <a name="how-to-use"></a>Cómo usar

1. Elige un framework abajo y haz clic en **Copiar JSON**.
2. En Spck Editor, abre `Ajustes > Editor > Snippets personalizados`.
3. Pulsa el menú y elige **Importar** (o pega en un nuevo archivo de snippets para ese lenguaje).
4. Los snippets aparecerán en la lista de autocompletado del editor mientras escribes su nombre de activación.

![Importar un paquete de snippets personalizado en Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Todos los snippets usan marcadores de posición de tabulación (`$1`, `$2`, `$0`) para que el cursor salte entre las posiciones editables tras la inserción. Consulta la [referencia de Snippets personalizados](./editor-lite#custom-snippets) para ver la sintaxis de marcadores.

## <a name="snippet-packs"></a>Paquetes de snippets

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), componentes funcionales y de flecha, hooks personalizados, forwardRef y patrones de Context Provider.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Descargar react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Scaffolding de App Router (page, layout, loading, error, not-found), manejadores de rutas, acciones de servidor, generateMetadata/StaticParams, Link, Image, importación dinámica, hooks de navegación y middleware.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Descargar nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitivas de Composition API, hooks de ciclo de vida, defineProps/Emits, store de Pinia y fallback de Options API (lado script) más scaffolding de SFC, v-for/v-if/v-model/v-bind/v-on, slots, transiciones y router-link (lado plantilla).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Descargar vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Declaraciones reactivas, ciclo de vida, todos los tipos de store y despachador de eventos (lado script) más andamiaje de componente, bloques {#if}/{#each}/{#await}/{#key}, directivas bind:/on:/class:/use:, suscripción a store y slots (lado plantilla).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Descargar svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Agrupaciones de utilidades comunes (diseños flex/grid, tarjetas, botones, entradas, badges, alertas), variantes responsive y de modo oscuro, más directivas CSS @apply/@layer/@tailwind.</p>
    <p>Modos de destino: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Descargar tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Andamiaje de app, todos los métodos HTTP, ruta asíncrona con try/catch, middleware, middleware de autenticación, manejador de errores, módulo Router, CORS, archivos estáticos y ayudantes de parámetros de solicitud.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Descargar express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Scaffolding de app, rutas GET/POST/PUT/DELETE, manejadores asíncronos, parámetros de ruta y consulta, modelos Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, subida de archivos y manejadores de ciclo de vida.</p>
    <p>Modo de destino: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Descargar fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modelos, vistas basadas en funciones y clases, DRF APIView/ViewSet/Serializer, formularios, urlpatterns, registro en el admin, migraciones, managers personalizados, señales y comandos de gestión.</p>
    <p>Modo de destino: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Descargar django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Copiar JSON</button>
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

## <a name="customizing"></a>Personalizar los snippets

Estos paquetes son puntos de partida — la mayoría de los equipos añaden sus propios patrones con el tiempo. Puedes editar cualquier snippet directamente dentro de la aplicación:

![Editar un snippet personalizado en Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Algunas adiciones útiles a considerar:

- **Andamiajes de componentes** que coincidan con la estructura de archivos de tu proyecto (p. ej., un snippet `page` que incluya tus importaciones estándar y el envoltorio de diseño).
- **Código de prueba repetitivo** — la estructura `describe`/`it` de tu framework de pruebas con las importaciones que siempre necesitas.
- **Llamadas de registro o telemetría** con los nombres de eventos específicos de tu proyecto ya rellenos.
- **Llamadas al cliente de API** — envuelve tu patrón estándar de llamadas `fetch`/axios/SDK con manejo de errores.

El formato JSON es sencillo — cada snippet es solo un `name` (lo que aparece en el autocompletado) y un cuerpo `snippet`. Edita el JSON descargado en cualquier editor de texto antes de importar.

## <a name="see-also"></a>Véase también

- [Referencia de Snippets personalizados](./editor-lite#custom-snippets) — sintaxis de marcadores, alcance y cómo gestionar snippets en la aplicación.
- [Primeros pasos](./editor) — instalación y descripción general de las funciones de Spck Editor.
