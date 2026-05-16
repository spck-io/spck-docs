# <a name="custom-snippets"></a>Extraits personnalisés

La fonctionnalité [Extraits personnalisés](./editor-lite#custom-snippets) de Spck Editor vous permet de définir des modèles de code réutilisables qui apparaissent dans la liste d’autocomplétion. Cette page propose des packs prêts à coller pour les motifs les plus courants des frameworks populaires, afin que vous n’ayez pas à écrire le code passe-partout vous-même.

> **Disponibilité :** Les Extraits personnalisés sont une fonctionnalité premium. Ils sont débloqués avec un [abonnement Gold](https://spck.io/pricing) dans la version complète de Spck Editor, ou via un achat unique avec [Spck Editor Lite](./editor-lite).

Chaque pack est une configuration JSON indexée par mode de langage (`javascript_ls` pour les frameworks frontend, `python_ls` pour ceux de Python, `html_ls`/`css_ls` pour les fragments de template et de style). Choisissez un framework, cliquez sur **Copier le JSON** et collez-le dans l’éditeur de configuration des extraits dans Spck Editor.

## <a name="how-to-use"></a>Comment l’utiliser

1. Choisissez un framework ci-dessous et cliquez sur **Copier le JSON**.
2. Dans Spck Editor, ouvrez `Settings > Editor > Custom Snippets`.
3. Touchez l’icône **Code** (en haut de la liste des extraits) pour modifier la configuration en JSON.
4. Collez le JSON copié, puis touchez **Update** pour écraser votre configuration d’extraits.
5. Les extraits apparaîtront dans la liste d’autocomplétion de votre éditeur lorsque vous taperez leur nom de déclencheur.

![Import d’un pack d’extraits personnalisés dans Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Tous les extraits utilisent des espaces réservés de tabulation (`$1`, `$2`, `$0`) afin que le curseur passe d’une position modifiable à l’autre après l’insertion. Consultez la [référence des Extraits personnalisés](./editor-lite#custom-snippets) pour la syntaxe des espaces réservés.

## <a name="snippet-packs"></a>Packs d’extraits

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), composants fonctionnels et fléchés, hooks personnalisés, forwardRef et motifs Context Provider.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Télécharger react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Squelette App Router (page, layout, loading, error, not-found), gestionnaires de route, server actions, generateMetadata/StaticParams, Link, Image, imports dynamiques, hooks de navigation et middleware.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Télécharger nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitives de la Composition API, hooks de cycle de vie, defineProps/Emits, store Pinia et repli sur l’Options API (côté script), ainsi que squelette SFC, v-for/v-if/v-model/v-bind/v-on, slots, transitions et router-link (côté template).</p>
    <p>Modes cibles : <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Télécharger vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Déclarations réactives, cycle de vie, tous les types de stores et event dispatcher (côté script), ainsi que squelette de composant, blocs {#if}/{#each}/{#await}/{#key}, directives bind:/on:/class:/use:, abonnement aux stores et slots (côté template).</p>
    <p>Modes cibles : <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Télécharger svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Regroupements d’utilitaires courants (layouts flex/grid, cartes, boutons, champs de saisie, badges, alertes), variantes responsive et mode sombre, ainsi que directives @apply/@layer/@tailwind côté CSS.</p>
    <p>Modes cibles : <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Télécharger tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Squelette d’application, toutes les méthodes HTTP, route asynchrone avec try/catch, middleware, middleware d’authentification, gestionnaire d’erreurs, module Router, CORS, fichiers statiques et utilitaires pour paramètres de requête.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Télécharger express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Squelette d’application, routes GET/POST/PUT/DELETE, handlers asynchrones, paramètres de chemin et de requête, modèles Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, téléversements de fichiers et handlers de lifespan.</p>
    <p>Mode cible : <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Télécharger fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modèles, vues basées sur fonctions et classes, DRF APIView/ViewSet/Serializer, formulaires, urlpatterns, enregistrement de l’admin, migrations, managers personnalisés, signaux et management commands.</p>
    <p>Mode cible : <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Télécharger django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Copier le JSON</button>
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

## <a name="customizing"></a>Personnaliser les extraits

Ces packs sont des points de départ — la plupart des développeurs ajoutent leurs propres motifs au fil du temps. Vous pouvez modifier n’importe quel extrait directement dans l’application :

![Modification d’un extrait personnalisé dans Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Ajouts utiles à envisager :

- **Squelettes de composants** correspondant à la structure de fichiers de votre projet (par exemple, un extrait `page` qui inclut vos imports standard et votre wrapper de layout).
- **Boilerplate de tests** — la structure `describe`/`it` de votre framework de tests avec les imports dont vous avez toujours besoin.
- **Appels de logging ou de télémétrie** avec les noms d’événements propres à votre projet pré-remplis.
- **Appels au client d’API** — encapsulez votre motif standard d’appel `fetch` / axios / SDK avec la gestion d’erreurs.

Le format JSON est simple — chaque extrait est juste un `name` (ce qui s’affiche dans l’autocomplétion) et un corps `snippet`. Modifiez le JSON téléchargé dans n’importe quel éditeur de texte avant de le coller dans la configuration des extraits.

## <a name="see-also"></a>Voir aussi

- [Référence des Extraits personnalisés](./editor-lite#custom-snippets) — syntaxe des espaces réservés, portée, et gestion des extraits dans l’application.
- [Spck Editor Lite](./editor-lite) — version à achat unique qui inclut les Extraits personnalisés.
- [Tarifs](https://spck.io/pricing) — détails de l’abonnement Gold pour la version complète de Spck Editor.
- [Premiers pas](./editor) — installation et aperçu des fonctionnalités de Spck Editor.
