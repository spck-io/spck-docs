# <a name="custom-snippets"></a>사용자 정의 스니펫

Spck Editor의 [사용자 정의 스니펫](./editor-lite#custom-snippets) 기능을 사용하면 자동 완성 목록에 표시되는 재사용 가능한 코드 템플릿을 정의할 수 있습니다. 이 페이지에서는 인기 있는 프레임워크에서 가장 흔히 쓰이는 패턴들에 대해 그대로 붙여 쓸 수 있는 스타터 팩을 제공하므로, 보일러플레이트 코드를 직접 작성하는 수고를 덜 수 있습니다.

> **이용 가능 조건:** 사용자 정의 스니펫은 프리미엄 기능입니다. Spck Editor 정식 버전에서는 [Gold 구독](https://spck.io/pricing)으로 잠금 해제되며, [Spck Editor Lite](./editor-lite)에서는 일회성 결제로 사용할 수 있습니다.

각 팩은 언어 모드별로 키가 지정된 JSON 설정입니다(프런트엔드 프레임워크는 `javascript_ls`, Python 계열은 `python_ls`, 템플릿 및 스타일 조각은 `html_ls`/`css_ls`). 프레임워크를 선택하고 **JSON 복사**를 누른 다음, Spck Editor의 스니펫 설정 편집기에 붙여넣으세요.

## <a name="how-to-use"></a>사용 방법

1. 아래에서 프레임워크를 선택하고 **JSON 복사**를 클릭합니다.
2. Spck Editor에서 `Settings > Editor > Custom Snippets`를 엽니다.
3. 스니펫 목록 상단의 **Code** 아이콘을 눌러 설정을 JSON으로 편집합니다.
4. 복사한 JSON을 붙여넣은 다음 **Update**를 눌러 스니펫 설정을 덮어씁니다.
5. 트리거 이름을 입력하면 편집기의 자동 완성 목록에 스니펫이 표시됩니다.

![Spck Editor에서 사용자 정의 스니펫 팩 가져오기](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

모든 스니펫은 탭 스톱 자리표시자(`$1`, `$2`, `$0`)를 사용하므로, 삽입 후 커서가 편집 가능한 위치 사이를 이동합니다. 자리표시자 구문은 [사용자 정의 스니펫 레퍼런스](./editor-lite#custom-snippets)를 참조하세요.

## <a name="snippet-packs"></a>스니펫 팩

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
    <p>훅(useState, useEffect, useRef, useMemo, useCallback, useContext, useReducer), 함수형 및 화살표 컴포넌트, 커스텀 훅, forwardRef, Context Provider 패턴.</p>
    <p>대상 모드: <code>javascript_ls</code> · <a href="/assets/snippets/react.json" download>react.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-react">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-react"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="nextjs">
    <p>App Router 골격(page, layout, loading, error, not-found), 라우트 핸들러, server actions, generateMetadata/StaticParams, Link, Image, 동적 import, 내비게이션 훅, 미들웨어.</p>
    <p>대상 모드: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 프리미티브, 라이프사이클 훅, defineProps/Emits, Pinia 스토어, Options API 대체 구문(스크립트 측)과 SFC 골격, v-for/v-if/v-model/v-bind/v-on, 슬롯, 트랜지션, router-link(템플릿 측).</p>
    <p>대상 모드: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>반응형 선언, 라이프사이클, 모든 스토어 유형, 이벤트 디스패처(스크립트 측)와 컴포넌트 골격, {#if}/{#each}/{#await}/{#key} 블록, bind:/on:/class:/use: 디렉티브, 스토어 구독, 슬롯(템플릿 측).</p>
    <p>대상 모드: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>자주 쓰는 유틸리티 조합(flex/grid 레이아웃, 카드, 버튼, 입력, 배지, 알림), 반응형 및 다크 모드 변형, CSS 측 @apply/@layer/@tailwind 디렉티브.</p>
    <p>대상 모드: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>앱 골격, 모든 HTTP 메서드, try/catch가 포함된 async 라우트, 미들웨어, 인증 미들웨어, 에러 핸들러, Router 모듈, CORS, 정적 파일, 요청 파라미터 헬퍼.</p>
    <p>대상 모드: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>앱 골격, GET/POST/PUT/DELETE 라우트, 비동기 핸들러, 경로 및 쿼리 파라미터, Pydantic 모델, Depends, HTTPException, APIRouter, BackgroundTasks, CORS 미들웨어, 파일 업로드, lifespan 핸들러.</p>
    <p>대상 모드: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>모델, 함수 기반 및 클래스 기반 뷰, DRF APIView/ViewSet/Serializer, 폼, urlpatterns, admin 등록, 마이그레이션, 커스텀 매니저, signals, management 커맨드.</p>
    <p>대상 모드: <code>python_ls</code> · <a href="/assets/snippets/django.json" download>django.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-django">JSON 복사</button>
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

## <a name="customizing"></a>스니펫 커스터마이징

이 팩들은 출발점일 뿐이며, 대부분의 개발자는 시간이 지나면서 자신만의 패턴을 추가합니다. 앱 내부에서 어떤 스니펫이든 직접 편집할 수 있습니다.

![Spck Editor에서 사용자 정의 스니펫 편집하기](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

추가하면 유용한 것들:

- 프로젝트의 파일 구조와 일치하는 **컴포넌트 골격**(예: 표준 import와 레이아웃 래퍼를 포함하는 `page` 스니펫).
- **테스트 보일러플레이트** — 항상 필요한 import가 포함된 테스트 프레임워크의 `describe`/`it` 구조.
- 프로젝트별 이벤트 이름이 미리 채워진 **로깅 또는 텔레메트리** 호출.
- **API 클라이언트 호출** — 에러 처리를 포함한 표준 `fetch` / axios / SDK 호출 패턴 래퍼.

JSON 포맷은 단순합니다 — 각 스니펫은 자동 완성에 표시되는 `name`과 본문 `snippet`으로만 구성됩니다. 다운로드한 JSON을 텍스트 편집기에서 수정한 뒤 스니펫 설정에 붙여넣으세요.

## <a name="see-also"></a>참고

- [사용자 정의 스니펫 레퍼런스](./editor-lite#custom-snippets) — 자리표시자 구문, 범위, 앱 내 스니펫 관리 방법.
- [Spck Editor Lite](./editor-lite) — 사용자 정의 스니펫이 포함된 일회성 결제 버전.
- [가격](https://spck.io/pricing) — Spck Editor 정식 버전을 위한 Gold 구독 상세 정보.
- [시작하기](./editor) — 설치 및 Spck Editor 기능 개요.
