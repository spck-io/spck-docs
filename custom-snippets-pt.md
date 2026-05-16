# <a name="custom-snippets"></a>Trechos personalizados

O recurso [Trechos personalizados](./editor-lite#custom-snippets) do Spck Editor permite definir modelos de código reutilizáveis que aparecem na lista de autocompletar. Esta página fornece pacotes iniciais prontos para colar com os padrões mais comuns dos frameworks populares — para que você não precise escrever o boilerplate por conta própria.

> **Disponibilidade:** Trechos personalizados é um recurso premium. Ele é desbloqueado com uma [assinatura Gold](https://spck.io/pricing) na versão completa do Spck Editor, ou como compra única pelo [Spck Editor Lite](./editor-lite).

Cada pacote é uma configuração JSON indexada por modo de linguagem (`javascript_ls` para os frameworks de frontend, `python_ls` para os de Python, `html_ls`/`css_ls` para fragmentos de template e estilo). Escolha um framework, clique em **Copiar JSON** e cole no editor de configuração de trechos no Spck Editor.

## <a name="how-to-use"></a>Como usar

1. Escolha um framework abaixo e clique em **Copiar JSON**.
2. No Spck Editor, abra `Settings > Editor > Custom Snippets`.
3. Toque no ícone **Code** (no topo da lista de trechos) para editar a configuração como JSON.
4. Cole o JSON copiado e, em seguida, toque em **Update** para sobrescrever sua configuração de trechos.
5. Os trechos aparecerão na lista de autocompletar do seu editor à medida que você digita o nome do gatilho.

![Importando um pacote de trechos personalizados no Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Todos os trechos usam marcadores de tabulação (`$1`, `$2`, `$0`) para que o cursor salte entre as posições editáveis após a inserção. Consulte a [referência de Trechos personalizados](./editor-lite#custom-snippets) para a sintaxe dos marcadores.

## <a name="snippet-packs"></a>Pacotes de trechos

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), componentes funcionais e de arrow, hooks personalizados, forwardRef e padrões de Context Provider.</p>
    <p>Modo alvo: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Baixar react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Estrutura de App Router (page, layout, loading, error, not-found), route handlers, server actions, generateMetadata/StaticParams, Link, Image, importação dinâmica, hooks de navegação e middleware.</p>
    <p>Modo alvo: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Baixar nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitivas da Composition API, hooks de ciclo de vida, defineProps/Emits, store do Pinia e fallback da Options API (lado do script), além da estrutura SFC, v-for/v-if/v-model/v-bind/v-on, slots, transições e router-link (lado do template).</p>
    <p>Modos alvo: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Baixar vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Declarações reativas, ciclo de vida, todos os tipos de store e event dispatcher (lado do script), além de estrutura de componente, blocos {#if}/{#each}/{#await}/{#key}, diretivas bind:/on:/class:/use:, assinatura de store e slots (lado do template).</p>
    <p>Modos alvo: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Baixar svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Agrupamentos comuns de utilitários (layouts flex/grid, cards, botões, inputs, badges, alertas), variantes responsivas e de modo escuro, além de diretivas @apply/@layer/@tailwind do lado CSS.</p>
    <p>Modos alvo: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Baixar tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Estrutura de app, todos os métodos HTTP, rota assíncrona com try/catch, middleware, middleware de autenticação, error handler, módulo Router, CORS, arquivos estáticos e helpers de parâmetros de requisição.</p>
    <p>Modo alvo: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Baixar express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Estrutura de app, rotas GET/POST/PUT/DELETE, handlers assíncronos, parâmetros de path e query, modelos Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, upload de arquivos e handlers de lifespan.</p>
    <p>Modo alvo: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Baixar fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Models, views baseadas em funções e classes, DRF APIView/ViewSet/Serializer, forms, urlpatterns, registro do admin, migrações, managers personalizados, signals e management commands.</p>
    <p>Modo alvo: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Baixar django.json</a></p>
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

## <a name="customizing"></a>Personalizando os trechos

Esses pacotes são pontos de partida — a maioria dos desenvolvedores adiciona seus próprios padrões ao longo do tempo. Você pode editar qualquer trecho diretamente dentro do aplicativo:

![Editando um trecho personalizado no Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Adições úteis a considerar:

- **Esqueletos de componentes** que correspondam à estrutura de arquivos do seu projeto (por exemplo, um trecho `page` que inclua seus imports padrão e o wrapper de layout).
- **Boilerplate de testes** — a estrutura `describe`/`it` do seu framework de testes com os imports que você sempre precisa.
- Chamadas de **logging ou telemetria** com os nomes de eventos específicos do seu projeto já preenchidos.
- **Chamadas a clientes de API** — envolva seu padrão padrão de chamada `fetch` / axios / SDK com tratamento de erros.

O formato JSON é simples — cada trecho é apenas um `name` (o que aparece no autocompletar) e um corpo `snippet`. Edite o JSON baixado em qualquer editor de texto antes de colá-lo na configuração de trechos.

## <a name="see-also"></a>Veja também

- [Referência de Trechos personalizados](./editor-lite#custom-snippets) — sintaxe de marcadores, escopo e como gerenciar trechos no aplicativo.
- [Spck Editor Lite](./editor-lite) — versão de compra única que inclui Trechos personalizados.
- [Preços](https://spck.io/pricing) — detalhes da assinatura Gold para a versão completa do Spck Editor.
- [Primeiros passos](./editor) — instalação e visão geral dos recursos do Spck Editor.
