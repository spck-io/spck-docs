# <a name="custom-snippets"></a>Fragmentos personalizados

La función [Fragmentos personalizados](./editor-lite#custom-snippets) de Spck Editor te permite definir plantillas de código reutilizables que aparecen en la lista de autocompletado. Esta página ofrece paquetes iniciales listos para pegar con los patrones más comunes de los frameworks más populares, para que no tengas que escribir el código repetitivo tú mismo.

> **Disponibilidad:** Fragmentos personalizados es una función premium. Se desbloquea con una [suscripción Gold](https://spck.io/pricing) en la versión completa de Spck Editor o mediante una compra única a través de [Spck Editor Lite](./editor-lite).

Cada paquete es una configuración JSON ordenada por modo de lenguaje (`javascript_ls` para los frameworks de frontend, `python_ls` para los de Python, `html_ls`/`css_ls` para fragmentos de plantilla y estilo). Elige un framework, pulsa **Copiar JSON** y pégalo en el editor de configuración de fragmentos de Spck Editor.

## <a name="how-to-use"></a>Cómo utilizarlo

1. Elige un framework de abajo y haz clic en **Copiar JSON**.
2. En Spck Editor, abre `Settings > Editor > Custom Snippets`.
3. Toca el icono **Code** (parte superior de la lista de fragmentos) para editar la configuración como JSON.
4. Pega el JSON copiado y luego toca **Update** para sobrescribir tu configuración de fragmentos.
5. Los fragmentos aparecerán en la lista de autocompletado de tu editor cuando escribas el nombre de su disparador.

![Importando un paquete de fragmentos personalizados en Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Todos los fragmentos utilizan marcadores de posición con paradas de tabulación (`$1`, `$2`, `$0`) para que el cursor salte entre las posiciones editables después de la inserción. Consulta la [referencia de Fragmentos personalizados](./editor-lite#custom-snippets) para conocer la sintaxis de los marcadores.

## <a name="snippet-packs"></a>Paquetes de fragmentos

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
    <p>Estructura de App Router (page, layout, loading, error, not-found), manejadores de ruta, server actions, generateMetadata/StaticParams, Link, Image, importación dinámica, hooks de navegación y middleware.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Descargar nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitivas de la Composition API, hooks de ciclo de vida, defineProps/Emits, store de Pinia y respaldo de Options API (lado del script), además de estructura SFC, v-for/v-if/v-model/v-bind/v-on, slots, transiciones y router-link (lado de la plantilla).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Descargar vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Declaraciones reactivas, ciclo de vida, todos los tipos de store y event dispatcher (lado del script), además de andamio de componente, bloques {#if}/{#each}/{#await}/{#key}, directivas bind:/on:/class:/use:, suscripción a stores y slots (lado de la plantilla).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Descargar svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Agrupaciones de utilidades comunes (layouts flex/grid, tarjetas, botones, entradas, badges, alertas), variantes responsive y de modo oscuro, además de directivas @apply/@layer/@tailwind del lado CSS.</p>
    <p>Modos de destino: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Descargar tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Estructura de app, todos los métodos HTTP, ruta asíncrona con try/catch, middleware, middleware de autenticación, manejador de errores, módulo Router, CORS, archivos estáticos y utilidades para parámetros de solicitud.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Descargar express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Estructura de app, rutas GET/POST/PUT/DELETE, handlers asíncronos, parámetros de ruta y consulta, modelos Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, cargas de archivos y handlers de lifespan.</p>
    <p>Modo de destino: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Descargar fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modelos, vistas basadas en funciones y clases, DRF APIView/ViewSet/Serializer, formularios, urlpatterns, registro de admin, migraciones, managers personalizados, signals y management commands.</p>
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

## <a name="customizing"></a>Personalizar los fragmentos

Estos paquetes son puntos de partida; la mayoría de los desarrolladores añaden sus propios patrones con el tiempo. Puedes editar cualquier fragmento directamente dentro de la app:

![Editando un fragmento personalizado en Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Añadidos útiles a considerar:

- **Andamios de componentes** que coincidan con la estructura de archivos de tu proyecto (por ejemplo, un fragmento `page` que incluya tus imports estándar y el envoltorio de layout).
- **Boilerplate de pruebas**: la estructura `describe`/`it` de tu framework de pruebas con los imports que siempre necesitas.
- **Llamadas de logging o telemetría** con los nombres de eventos específicos de tu proyecto ya rellenados.
- **Llamadas a clientes de API**: encapsula tu patrón estándar de `fetch` / axios / SDK con manejo de errores.

El formato JSON es sencillo: cada fragmento es solo un `name` (lo que se muestra en el autocompletado) y un cuerpo `snippet`. Edita el JSON descargado en cualquier editor de texto antes de pegarlo en la configuración de fragmentos.

## <a name="see-also"></a>Véase también

- [Referencia de Fragmentos personalizados](./editor-lite#custom-snippets): sintaxis de marcadores, ámbito y cómo gestionar fragmentos en la app.
- [Spck Editor Lite](./editor-lite): versión de compra única que incluye Fragmentos personalizados.
- [Precios](https://spck.io/pricing): detalles de la suscripción Gold para la versión completa de Spck Editor.
- [Primeros pasos](./editor): instalación y resumen de las funciones de Spck Editor.
