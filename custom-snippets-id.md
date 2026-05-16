# <a name="custom-snippets"></a>Cuplikan Khusus

Fitur [Cuplikan Khusus](./editor-lite#custom-snippets) di Spck Editor memungkinkan Anda menentukan templat kode yang dapat digunakan kembali dan muncul di daftar pelengkapan otomatis. Halaman ini menyediakan paket pemula siap tempel untuk pola paling umum di berbagai framework populer — sehingga Anda tidak perlu menulis kode boilerplate sendiri.

> **Ketersediaan:** Cuplikan Khusus adalah fitur premium. Fitur ini terbuka dengan [langganan Gold](https://spck.io/pricing) di Spck Editor versi penuh, atau melalui pembelian sekali bayar lewat [Spck Editor Lite](./editor-lite).

Setiap paket adalah konfigurasi JSON yang dikelompokkan berdasarkan mode bahasa (`javascript_ls` untuk framework frontend, `python_ls` untuk Python, `html_ls`/`css_ls` untuk fragmen templat dan gaya). Pilih framework, klik **Salin JSON**, lalu tempel ke editor konfigurasi cuplikan di Spck Editor.

## <a name="how-to-use"></a>Cara Menggunakan

1. Pilih framework di bawah dan klik **Salin JSON**.
2. Di Spck Editor, buka `Settings > Editor > Custom Snippets`.
3. Ketuk ikon **Code** (di bagian atas daftar cuplikan) untuk mengedit konfigurasi sebagai JSON.
4. Tempel JSON yang sudah disalin, lalu ketuk **Update** untuk menimpa konfigurasi cuplikan Anda.
5. Cuplikan akan muncul di daftar pelengkapan otomatis editor Anda saat Anda mengetik nama pemicunya.

![Mengimpor paket cuplikan khusus di Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

Semua cuplikan menggunakan placeholder tab-stop (`$1`, `$2`, `$0`) sehingga kursor berpindah antar posisi yang dapat diedit setelah penyisipan. Lihat [referensi Cuplikan Khusus](./editor-lite#custom-snippets) untuk sintaks placeholder.

## <a name="snippet-packs"></a>Paket Cuplikan

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
    <p>Hooks (useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), komponen fungsional dan arrow, custom hooks, forwardRef, dan pola Context Provider.</p>
    <p>Mode target: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>Unduh react.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>Kerangka App Router (page, layout, loading, error, not-found), route handler, server actions, generateMetadata/StaticParams, Link, Image, dynamic import, hook navigasi, dan middleware.</p>
    <p>Mode target: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>Unduh nextjs.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Primitif Composition API, hook siklus hidup, defineProps/Emits, store Pinia, dan fallback Options API (sisi script) ditambah kerangka SFC, v-for/v-if/v-model/v-bind/v-on, slot, transisi, dan router-link (sisi template).</p>
    <p>Mode target: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>Unduh vue.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>Deklarasi reaktif, siklus hidup, semua jenis store, dan event dispatcher (sisi script) ditambah kerangka komponen, blok {#if}/{#each}/{#await}/{#key}, direktif bind:/on:/class:/use:, langganan store, dan slot (sisi template).</p>
    <p>Mode target: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>Unduh svelte.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>Pengelompokan utilitas umum (tata letak flex/grid, kartu, tombol, input, badge, alert), varian responsif dan mode gelap, plus direktif @apply/@layer/@tailwind sisi CSS.</p>
    <p>Mode target: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>Unduh tailwind.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>Kerangka app, semua metode HTTP, route async dengan try/catch, middleware, middleware autentikasi, error handler, modul Router, CORS, file statis, dan helper parameter request.</p>
    <p>Mode target: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>Unduh express.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>Kerangka app, route GET/POST/PUT/DELETE, handler async, parameter path dan query, model Pydantic, Depends, HTTPException, APIRouter, BackgroundTasks, middleware CORS, upload file, dan handler lifespan.</p>
    <p>Mode target: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>Unduh fastapi.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">Salin JSON</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>Model, view berbasis fungsi dan kelas, DRF APIView/ViewSet/Serializer, form, urlpatterns, registrasi admin, migrasi, manager kustom, signals, dan management command.</p>
    <p>Mode target: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>Unduh django.json</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">Salin JSON</button>
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

## <a name="customizing"></a>Menyesuaikan Cuplikan

Paket-paket ini adalah titik awal — kebanyakan developer menambahkan pola mereka sendiri seiring waktu. Anda dapat mengedit cuplikan apa pun langsung di dalam aplikasi:

![Mengedit cuplikan khusus di Spck Editor](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

Tambahan yang bermanfaat untuk dipertimbangkan:

- **Kerangka komponen** yang sesuai dengan struktur file proyek Anda (mis. cuplikan `page` yang mencakup import standar dan layout wrapper Anda).
- **Boilerplate pengujian** — struktur `describe`/`it` framework pengujian Anda dengan import yang selalu Anda perlukan.
- **Pemanggilan logging atau telemetri** dengan nama event khusus proyek Anda yang sudah terisi.
- **Pemanggilan client API** — bungkus pola pemanggilan standar `fetch` / axios / SDK Anda dengan penanganan error.

Format JSON ini sederhana — setiap cuplikan hanya berupa `name` (yang muncul di pelengkapan otomatis) dan body `snippet`. Edit JSON yang diunduh di editor teks apa pun sebelum menempelkannya ke konfigurasi cuplikan.

## <a name="see-also"></a>Lihat Juga

- [Referensi Cuplikan Khusus](./editor-lite#custom-snippets) — sintaks placeholder, cakupan, dan cara mengelola cuplikan di dalam aplikasi.
- [Spck Editor Lite](./editor-lite) — versi pembelian sekali bayar yang menyertakan Cuplikan Khusus.
- [Harga](https://spck.io/pricing) — detail langganan Gold untuk Spck Editor versi penuh.
- [Memulai](./editor) — pemasangan dan ikhtisar fitur Spck Editor.
