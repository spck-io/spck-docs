# <a name="custom-snippets"></a>Extraits de code personnalisés de démarrage

La fonctionnalité [Extraits de code personnalisés](./editor-lite#custom-snippets) de Spck Editor vous permet de définir des modèles de code réutilisables qui s'affichent dans la liste d'autocomplétion. Cette page propose des packs de démarrage prêts à coller pour les modèles les plus courants dans les frameworks populaires — afin que vous n'ayez pas à écrire le code standard vous-même.

Chaque pack est une configuration JSON organisée par mode de langage (`javascript_ls` pour les frameworks frontend, `python_ls` pour ceux en Python, `html_ls`/`css_ls` pour les fragments de gabarit et de style). Choisissez un framework, cliquez sur **Copier** et collez dans `Paramètres > Éditeur > Extraits de code personnalisés > Importer`.

## <a name="how-to-use"></a>Comment utiliser

1. Choisissez un framework ci-dessous et cliquez sur **Copier le JSON**.
2. Dans Spck Editor, ouvrez `Paramètres > Éditeur > Extraits de code personnalisés`.
3. Appuyez sur le menu et choisissez **Importer** (ou collez dans un nouveau fichier d'extraits pour ce langage).
4. Les extraits apparaîtront dans la liste d'autocomplétion de l'éditeur au fur et à mesure que vous tapez leur nom de déclenchement.

![Importation d'un pack d'extraits personnalisés dans Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Tous les extraits utilisent des espaces réservés de tabulation (`$1`, `$2`, `$0`) pour que le curseur saute entre les positions éditables après l'insertion. Consultez la [référence des Extraits de code personnalisés](./editor-lite#custom-snippets) pour la syntaxe des espaces réservés.

## <a name="snippet-packs"></a>Packs d'extraits

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), composants fonctionnels et fléchés, hooks personnalisés, forwardRef et modèles de Context Provider.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Télécharger react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Scaffolding App Router (page, layout, loading, error, not-found), gestionnaires de routes, actions serveur, generateMetadata/StaticParams, Link, Image, import dynamique, hooks de navigation et middleware.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Télécharger nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitives de l'API de composition, hooks de cycle de vie, defineProps/Emits, store Pinia et repli Options API (côté script) plus scaffolding SFC, v-for/v-if/v-model/v-bind/v-on, slots, transitions et router-link (côté gabarit).</p>
    <p>Modes cibles : <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Télécharger vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Déclarations réactives, cycle de vie, tous les types de store et le dispatcher d'événements (côté script) plus le squelette de composant, les blocs {#if}/{#each}/{#await}/{#key}, les directives bind:/on:/class:/use:, les abonnements aux stores et les slots (côté gabarit).</p>
    <p>Modes cibles : <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Télécharger svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Groupements d'utilitaires courants (mises en page flex/grid, cartes, boutons, champs de saisie, badges, alertes), variantes responsive et mode sombre, plus les directives CSS @apply/@layer/@tailwind.</p>
    <p>Modes cibles : <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Télécharger tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Squelette d'application, toutes les méthodes HTTP, route asynchrone avec try/catch, middleware, middleware d'authentification, gestionnaire d'erreurs, module Router, CORS, fichiers statiques et helpers de paramètres de requête.</p>
    <p>Mode cible : <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Télécharger express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Scaffolding d'application, routes GET/POST/PUT/DELETE, gestionnaires asynchrones, paramètres de chemin et de requête, modèles Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, téléchargements de fichiers et gestionnaires de cycle de vie.</p>
    <p>Mode cible : <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Télécharger fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copier le JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modèles, vues basées sur des fonctions et des classes, DRF APIView/ViewSet/Serializer, formulaires, urlpatterns, enregistrement admin, migrations, managers personnalisés, signaux et commandes de gestion.</p>
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

Ces packs sont des points de départ — la plupart des équipes ajoutent leurs propres modèles au fil du temps. Vous pouvez modifier n'importe quel extrait directement dans l'application :

![Modification d'un extrait de code personnalisé dans Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Ajouts utiles à envisager :

- **Gabarits de composants** correspondant à la structure de fichiers de votre projet (par ex. un extrait `page` qui inclut vos imports standard et votre wrapper de mise en page).
- **Code standard de test** — la structure `describe`/`it` de votre framework de test avec les imports dont vous avez toujours besoin.
- **Appels de journalisation ou de télémétrie** avec les noms d'événements spécifiques à votre projet pré-remplis.
- **Appels au client API** — encapsulez votre modèle d'appel standard `fetch`/axios/SDK avec gestion des erreurs.

Le format JSON est simple — chaque extrait n'est qu'un `name` (ce qui s'affiche dans l'autocomplétion) et un corps `snippet`. Modifiez le JSON téléchargé dans n'importe quel éditeur de texte avant d'importer.

## <a name="see-also"></a>Voir aussi

- [Référence des Extraits de code personnalisés](./editor-lite#custom-snippets) — syntaxe des espaces réservés, portée et gestion des extraits dans l'application.
- [Premiers pas](./editor) — installation et aperçu des fonctionnalités de Spck Editor.
