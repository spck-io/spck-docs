# <a name="custom-snippets"></a>Snippets Personalizados para Começar

O recurso [Snippets Personalizados](./editor-lite#custom-snippets) do Spck Editor permite definir modelos de código reutilizáveis que aparecem na lista de autocompletar. Esta página fornece pacotes de início prontos para colar com os padrões mais comuns nos frameworks populares — para que você não precise escrever o código repetitivo sozinho.

Cada pacote é uma configuração JSON organizada por modo de linguagem (`javascript_ls` para os frameworks frontend, `python_ls` para os de Python, `html_ls`/`css_ls` para fragmentos de template e estilo). Escolha um framework, clique em **Copiar** e cole em `Configurações > Editor > Snippets Personalizados > Importar`.

## <a name="how-to-use"></a>Como Usar

1. Escolha um framework abaixo e clique em **Copiar JSON**.
2. No Spck Editor, abra `Configurações > Editor > Snippets Personalizados`.
3. Toque no menu e escolha **Importar** (ou cole em um novo arquivo de snippet para aquela linguagem).
4. Os snippets aparecerão na lista de autocompletar do editor conforme você digitar o nome de ativação.

![Importando um pacote de snippets personalizado no Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Todos os snippets usam marcadores de posição de tabulação (`$1`, `$2`, `$0`) para que o cursor salte entre as posições editáveis após a inserção. Consulte a [referência de Snippets Personalizados](./editor-lite#custom-snippets) para a sintaxe dos marcadores.

## <a name="snippet-packs"></a>Pacotes de Snippets

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), componentes funcionais e de seta, hooks personalizados, forwardRef e padrões de Context Provider.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Baixar react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Scaffolding do App Router (page, layout, loading, error, not-found), manipuladores de rota, ações do servidor, generateMetadata/StaticParams, Link, Image, importação dinâmica, hooks de navegação e middleware.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Baixar nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitivos da Composition API, hooks de ciclo de vida, defineProps/Emits, store Pinia e fallback da Options API (lado script) mais scaffolding de SFC, v-for/v-if/v-model/v-bind/v-on, slots, transições e router-link (lado template).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Baixar vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Declarações reativas, ciclo de vida, todos os tipos de store e despachador de eventos (lado script) mais andaime de componente, blocos {#if}/{#each}/{#await}/{#key}, diretivas bind:/on:/class:/use:, assinatura de store e slots (lado template).</p>
    <p>Modos de destino: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Baixar svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Agrupamentos de utilitários comuns (layouts flex/grid, cartões, botões, entradas, badges, alertas), variantes responsivas e de modo escuro, mais diretivas CSS @apply/@layer/@tailwind.</p>
    <p>Modos de destino: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Baixar tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Andaime de app, todos os métodos HTTP, rota assíncrona com try/catch, middleware, middleware de autenticação, manipulador de erros, módulo Router, CORS, arquivos estáticos e helpers de parâmetros de requisição.</p>
    <p>Modo de destino: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Baixar express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Scaffolding de app, rotas GET/POST/PUT/DELETE, manipuladores assíncronos, parâmetros de caminho e query, modelos Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, upload de arquivos e manipuladores de ciclo de vida.</p>
    <p>Modo de destino: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Baixar fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Copiar JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Modelos, views baseadas em funções e classes, DRF APIView/ViewSet/Serializer, formulários, urlpatterns, registro no admin, migrações, managers personalizados, signals e comandos de gerenciamento.</p>
    <p>Modo de destino: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Baixar django.json</a></p>
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

## <a name="customizing"></a>Personalizando os Snippets

Estes pacotes são pontos de partida — a maioria das equipes adiciona seus próprios padrões ao longo do tempo. Você pode editar qualquer snippet diretamente dentro do aplicativo:

![Editando um snippet personalizado no Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Adições úteis a considerar:

- **Andaimes de componentes** que correspondam à estrutura de arquivos do seu projeto (p. ex., um snippet `page` que inclua seus imports padrão e o wrapper de layout).
- **Boilerplate de testes** — a estrutura `describe`/`it` do seu framework de testes com os imports que você sempre precisa.
- **Chamadas de logging ou telemetria** com os nomes de eventos específicos do seu projeto já preenchidos.
- **Chamadas ao cliente de API** — envolva seu padrão padrão de chamadas `fetch`/axios/SDK com tratamento de erros.

O formato JSON é simples — cada snippet é apenas um `name` (o que aparece no autocompletar) e um corpo `snippet`. Edite o JSON baixado em qualquer editor de texto antes de importar.

## <a name="see-also"></a>Veja Também

- [Referência de Snippets Personalizados](./editor-lite#custom-snippets) — sintaxe de marcadores, escopo e como gerenciar snippets no aplicativo.
- [Primeiros Passos](./editor) — instalação e visão geral das funcionalidades do Spck Editor.
