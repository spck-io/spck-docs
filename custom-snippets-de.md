# <a name="custom-snippets"></a>Starter-Codeausschnitte

Spck Editors Funktion [Benutzerdefinierte Codeausschnitte](./editor-lite#custom-snippets) ermöglicht es dir, wiederverwendbare Code-Vorlagen zu definieren, die in der Autovervollständigungsliste erscheinen. Diese Seite bietet sofort einsatzbereite Starterpakete für die häufigsten Muster in den beliebtesten Frameworks — damit du dir das Boilerplate selbst schreiben sparst.

Jedes Paket ist eine JSON-Konfiguration, geordnet nach Sprachmodus (`javascript_ls` für die Frontend-Frameworks, `python_ls` für die Python-Varianten, `html_ls`/`css_ls` für Template- und Style-Fragmente). Wähle ein Framework, klicke auf **Kopieren** und füge es unter `Einstellungen > Editor > Benutzerdefinierte Codeausschnitte > Importieren` ein.

## <a name="how-to-use"></a>Verwendung

1. Wähle unten ein Framework aus und klicke auf **JSON kopieren**.
2. Öffne in Spck Editor `Einstellungen > Editor > Benutzerdefinierte Codeausschnitte`.
3. Tippe auf das Menü und wähle **Importieren** (oder füge den Inhalt in eine neue Snippet-Datei für diese Sprache ein).
4. Die Codeausschnitte erscheinen in der Autovervollständigungsliste des Editors, sobald du ihren Auslösenamen eingibst.

![Importieren eines benutzerdefinierten Snippet-Pakets in Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Alle Codeausschnitte verwenden Tab-Stop-Platzhalter (`$1`, `$2`, `$0`), sodass der Cursor nach der Einfügung zwischen den bearbeitbaren Positionen springt. Weitere Informationen zur Platzhaltersyntax findest du in der [Referenz für benutzerdefinierte Codeausschnitte](./editor-lite#custom-snippets).

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), funktionale und Arrow-Komponenten, eigene Hooks, forwardRef und Context-Provider-Muster.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>react.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App-Router-Gerüste (page, layout, loading, error, not-found), Route-Handler, Server-Actions, generateMetadata/StaticParams, Link, Image, Dynamic Import, Navigations-Hooks und Middleware.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition-API-Primitive, Lifecycle-Hooks, defineProps/Emits, Pinia-Store und Options-API-Fallback (Script-Seite) sowie SFC-Gerüst, v-for/v-if/v-model/v-bind/v-on, Slots, Übergänge und router-link (Template-Seite).</p>
    <p>Zielmodi: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Reaktive Deklarationen, Lifecycle, alle Store-Typen und Event-Dispatcher (Script-Seite) sowie Komponenten-Gerüst, {#if}/{#each}/{#await}/{#key}-Blöcke, bind:/on:/class:/use:-Direktiven, Store-Abonnement und Slots (Template-Seite).</p>
    <p>Zielmodi: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Häufige Utility-Gruppen (Flex-/Grid-Layouts, Karten, Buttons, Eingabefelder, Badges, Alerts), responsive und Dark-Mode-Varianten sowie CSS-seitige @apply/@layer/@tailwind-Direktiven.</p>
    <p>Zielmodi: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>App-Gerüst, alle HTTP-Methoden, asynchrone Route mit try/catch, Middleware, Auth-Middleware, Error-Handler, Router-Modul, CORS, statische Dateien und Request-Parameter-Helfer.</p>
    <p>Zielmodus: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>App-Gerüst, GET/POST/PUT/DELETE-Routen, asynchrone Handler, Pfad- und Query-Parameter, Pydantic-Modelle, Depends, HTTPException, APIRouter, BackgroundTasks, CORS-Middleware, Datei-Uploads und Lifespan-Handler.</p>
    <p>Zielmodus: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.json herunterladen</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSON kopieren</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modelle, funktions- und klassenbasierte Views, DRF APIView/ViewSet/Serializer, Formulare, urlpatterns, Admin-Registrierung, Migrationen, benutzerdefinierte Manager, Signale und Verwaltungsbefehle.</p>
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

## <a name="customizing"></a>Codeausschnitte anpassen

Diese Pakete sind Ausgangspunkte — die meisten Teams fügen im Laufe der Zeit eigene Muster hinzu. Du kannst jeden Codeausschnitt direkt in der App bearbeiten:

![Bearbeiten eines benutzerdefinierten Codeausschnitts in Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Nützliche Ergänzungen:

- **Komponenten-Gerüste** passend zur Dateistruktur deines Projekts (z. B. ein `page`-Snippet mit deinen Standardimporten und dem Layout-Wrapper).
- **Test-Boilerplate** — die `describe`/`it`-Struktur deines Test-Frameworks mit den stets benötigten Importen.
- **Protokollierungs- oder Telemetrieaufrufe** mit vorausgefüllten projektspezifischen Ereignisnamen.
- **API-Client-Aufrufe** — kapsle dein Standard-`fetch`/axios/SDK-Aufrufmuster mit Fehlerbehandlung.

Das JSON-Format ist unkompliziert — jeder Codeausschnitt besteht nur aus einem `name` (was in der Autovervollständigung erscheint) und einem `snippet`-Body. Bearbeite die heruntergeladene JSON-Datei in einem beliebigen Texteditor vor dem Importieren.

## <a name="see-also"></a>Siehe auch

- [Referenz für benutzerdefinierte Codeausschnitte](./editor-lite#custom-snippets) — Platzhaltersyntax, Geltungsbereiche und Verwaltung von Codeausschnitten in der App.
- [Erste Schritte](./editor) — Installation und ein Überblick über die Funktionen von Spck Editor.
