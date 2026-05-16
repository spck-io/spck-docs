# <a name="custom-snippets"></a>Benutzerdefinierte Snippets

Die Funktion [Benutzerdefinierte Snippets](./editor-lite#custom-snippets) von Spck Editor ermöglicht es Ihnen, wiederverwendbare Codevorlagen zu definieren, die in der Autocomplete-Liste erscheinen. Diese Seite bietet einsatzbereite Starter-Pakete für die häufigsten Muster der beliebtesten Frameworks – damit Sie sich das Schreiben des Boilerplate-Codes sparen können.

> **Verfügbarkeit:** Benutzerdefinierte Snippets ist eine Premium-Funktion. Sie wird mit einem [Gold-Abonnement](https://spck.io/pricing) in der Vollversion von Spck Editor freigeschaltet oder als Einmalkauf über [Spck Editor Lite](./editor-lite).

Jedes Paket ist eine JSON-Konfiguration, die nach Sprachmodus gegliedert ist (`javascript_ls` für die Frontend-Frameworks, `python_ls` für die Python-Frameworks, `html_ls`/`css_ls` für Template- und Style-Fragmente). Wählen Sie ein Framework, klicken Sie auf **JSON kopieren** und fügen Sie es im Snippet-Konfigurationseditor in Spck Editor ein.

## <a name="how-to-use"></a>Verwendung

1. Wählen Sie unten ein Framework und klicken Sie auf **JSON kopieren**.
2. Öffnen Sie in Spck Editor `Settings > Editor > Custom Snippets`.
3. Tippen Sie auf das **Code**-Symbol (oben in der Snippet-Liste), um die Konfiguration als JSON zu bearbeiten.
4. Fügen Sie das kopierte JSON ein und tippen Sie dann auf **Update**, um Ihre Snippet-Konfiguration zu überschreiben.
5. Die Snippets erscheinen in der Autocomplete-Liste Ihres Editors, sobald Sie deren Auslösernamen eingeben.

![Importieren eines benutzerdefinierten Snippet-Pakets in Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Alle Snippets verwenden Tab-Stopp-Platzhalter (`$1`, `$2`, `$0`), sodass der Cursor nach dem Einfügen zwischen den bearbeitbaren Positionen springt. Siehe die [Referenz für Benutzerdefinierte Snippets](./editor-lite#custom-snippets) für die Platzhalter-Syntax.

## <a name="snippet-packs"></a>Snippet-Pakete

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), funktionale und Arrow-Komponenten, Custom Hooks, forwardRef und Context-Provider-Muster.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>react.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App-Router-Gerüst (page, layout, loading, error, not-found), Route-Handler, Server-Actions, generateMetadata/StaticParams, Link, Image, dynamische Imports, Navigations-Hooks und Middleware.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition-API-Primitive, Lifecycle-Hooks, defineProps/Emits, Pinia-Store und Options-API-Fallback (Skriptseite) sowie SFC-Gerüst, v-for/v-if/v-model/v-bind/v-on, Slots, Transitions und router-link (Templateseite).</p>
    <p>Zielmodi: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Reaktive Deklarationen, Lifecycle, alle Store-Typen und Event-Dispatcher (Skriptseite) sowie Komponentengerüst, {#if}/{#each}/{#await}/{#key}-Blöcke, bind:/on:/class:/use:-Direktiven, Store-Abonnement und Slots (Templateseite).</p>
    <p>Zielmodi: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Häufige Utility-Gruppierungen (flex/grid-Layouts, Karten, Buttons, Eingabefelder, Badges, Alerts), responsive und Dark-Mode-Varianten sowie CSS-seitige @apply/@layer/@tailwind-Direktiven.</p>
    <p>Zielmodi: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>App-Gerüst, alle HTTP-Methoden, async Route mit try/catch, Middleware, Auth-Middleware, Error-Handler, Router-Modul, CORS, statische Dateien und Hilfsfunktionen für Request-Parameter.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>App-Gerüst, GET/POST/PUT/DELETE-Routen, async Handler, Path- und Query-Parameter, Pydantic-Modelle, Depends, HTTPException, APIRouter, BackgroundTasks, CORS-Middleware, Datei-Uploads und Lifespan-Handler.</p>
    <p>Zielmodus: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modelle, funktionsbasierte und klassenbasierte Views, DRF APIView/ViewSet/Serializer, Formulare, urlpatterns, Admin-Registrierung, Migrationen, Custom Manager, Signals und Management Commands.</p>
    <p>Zielmodus: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>django.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">JSON kopieren</button>
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

## <a name="customizing"></a>Snippets anpassen

Diese Pakete sind nur Ausgangspunkte – die meisten Entwickler fügen mit der Zeit eigene Muster hinzu. Sie können jedes Snippet direkt in der App bearbeiten:

![Bearbeiten eines benutzerdefinierten Snippets in Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Nützliche Ergänzungen, die in Betracht zu ziehen sind:

- **Komponentengerüste**, die zur Dateistruktur Ihres Projekts passen (z. B. ein `page`-Snippet, das Ihre Standard-Imports und Ihren Layout-Wrapper enthält).
- **Test-Boilerplate** – die `describe`/`it`-Struktur Ihres Test-Frameworks mit den Imports, die Sie immer benötigen.
- **Logging- oder Telemetrie-Aufrufe** mit Ihren projektspezifischen Event-Namen vorausgefüllt.
- **API-Client-Aufrufe** – verpacken Sie Ihr Standard-`fetch`-/axios-/SDK-Aufrufmuster mit Fehlerbehandlung.

Das JSON-Format ist einfach – jedes Snippet besteht nur aus einem `name` (was in der Autocomplete-Liste erscheint) und einem `snippet`-Body. Bearbeiten Sie das heruntergeladene JSON in einem beliebigen Texteditor, bevor Sie es in die Snippet-Konfiguration einfügen.

## <a name="see-also"></a>Siehe auch

- [Referenz für Benutzerdefinierte Snippets](./editor-lite#custom-snippets) – Platzhalter-Syntax, Geltungsbereich und wie Sie Snippets in der App verwalten.
- [Spck Editor Lite](./editor-lite) – Einmalkauf-Version, die Benutzerdefinierte Snippets enthält.
- [Preise](https://spck.io/pricing) – Details zum Gold-Abonnement für die Vollversion von Spck Editor.
- [Erste Schritte](./editor) – Installation und Überblick über die Funktionen von Spck Editor.
