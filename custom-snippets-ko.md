# <a name="custom-snippets"></a>커스텀 스니펫 스타터 팩

Spck Editor의 [커스텀 스니펫](./editor-lite#custom-snippets) 기능을 사용하면 자동 완성 목록에 표시되는 재사용 가능한 코드 템플릿을 정의할 수 있습니다. 이 페이지에서는 인기 있는 프레임워크에서 가장 일반적인 패턴에 대한 바로 붙여넣기 가능한 스타터 팩을 제공합니다 — 보일러플레이트 코드를 직접 작성할 필요가 없습니다.

각 팩은 언어 모드별로 구성된 JSON 설정입니다(프론트엔드 프레임워크에는 `javascript_ls`, Python에는 `python_ls`, 템플릿 및 스타일 조각에는 `html_ls`/`css_ls`). 프레임워크를 선택하고 **복사**를 클릭한 다음 `설정 > 에디터 > 커스텀 스니펫 > 가져오기`에 붙여넣으세요.

## <a name="how-to-use"></a>사용 방법

1. 아래에서 프레임워크를 선택하고 **JSON 복사**를 클릭합니다.
2. Spck Editor에서 `설정 > 에디터 > 커스텀 스니펫`을 엽니다.
3. 메뉴를 탭하고 **가져오기**를 선택합니다(또는 해당 언어의 새 스니펫 파일에 붙여넣습니다).
4. 트리거 이름을 입력하면 에디터의 자동 완성 목록에 스니펫이 표시됩니다.

![Spck Editor에서 커스텀 스니펫 팩 가져오기](https://docs.spck.io/assets/gifs/custom-snippet-import.gif)

모든 스니펫은 탭 스톱 플레이스홀더(`$1`, `$2`, `$0`)를 사용하여 삽입 후 커서가 편집 가능한 위치 사이를 이동합니다. 플레이스홀더 구문에 대한 자세한 내용은 [커스텀 스니펫 참조](./editor-lite#custom-snippets)를 확인하세요.

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
    <p>App Router 스캐폴딩(page, layout, loading, error, not-found), 라우트 핸들러, 서버 액션, generateMetadata/StaticParams, Link, Image, 동적 임포트, 내비게이션 훅, 미들웨어.</p>
    <p>대상 모드: <code>javascript_ls</code> · <a href="/assets/snippets/nextjs.json" download>nextjs.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-nextjs">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-nextjs"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="vue">
    <p>Composition API 기본형, 라이프사이클 훅, defineProps/Emits, Pinia 스토어, Options API 폴백(스크립트 측) 및 SFC 스캐폴딩, v-for/v-if/v-model/v-bind/v-on, 슬롯, 트랜지션, router-link(템플릿 측).</p>
    <p>대상 모드: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/vue.json" download>vue.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-vue">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-vue"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="svelte">
    <p>반응형 선언, 라이프사이클, 모든 스토어 유형, 이벤트 디스패처(스크립트 측) 및 컴포넌트 스캐폴드, {#if}/{#each}/{#await}/{#key} 블록, bind:/on:/class:/use: 지시어, 스토어 구독, 슬롯(템플릿 측).</p>
    <p>대상 모드: <code>javascript_ls</code> + <code>html_ls</code> · <a href="/assets/snippets/svelte.json" download>svelte.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-svelte">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-svelte"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="tailwind">
    <p>일반적인 유틸리티 그룹(flex/grid 레이아웃, 카드, 버튼, 입력 필드, 배지, 알림), 반응형 및 다크 모드 변형, CSS 측 @apply/@layer/@tailwind 지시어.</p>
    <p>대상 모드: <code>html_ls</code> + <code>css_ls</code> · <a href="/assets/snippets/tailwind.json" download>tailwind.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-tailwind">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-tailwind"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="express">
    <p>앱 스캐폴드, 모든 HTTP 메서드, try/catch가 있는 비동기 라우트, 미들웨어, 인증 미들웨어, 오류 처리기, Router 모듈, CORS, 정적 파일 및 요청 파라미터 헬퍼.</p>
    <p>대상 모드: <code>javascript_ls</code> · <a href="/assets/snippets/express.json" download>express.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-express">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-express"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="fastapi">
    <p>앱 스캐폴딩, GET/POST/PUT/DELETE 라우트, 비동기 핸들러, 경로 및 쿼리 파라미터, Pydantic 모델, Depends, HTTPException, APIRouter, BackgroundTasks, CORS 미들웨어, 파일 업로드 및 수명 주기 핸들러.</p>
    <p>대상 모드: <code>python_ls</code> · <a href="/assets/snippets/fastapi.json" download>fastapi.json 다운로드</a></p>
    <div class="snippet-copy-wrap">
      <button type="button" class="snippet-copy-btn" data-target="snippet-json-fastapi">JSON 복사</button>
      <pre><code class="hljs" id="snippet-json-fastapi"></code></pre>
    </div>
  </div>

  <div class="snippet-tab-pane" data-pack="django">
    <p>모델, 함수 및 클래스 기반 뷰, DRF APIView/ViewSet/Serializer, 폼, urlpatterns, 관리자 등록, 마이그레이션, 커스텀 매니저, 시그널 및 관리 명령어.</p>
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

이 팩들은 출발점입니다 — 대부분의 팀은 시간이 지나면서 자체 패턴을 추가합니다. 앱 내에서 직접 스니펫을 편집할 수 있습니다:

![Spck Editor에서 커스텀 스니펫 편집하기](https://docs.spck.io/assets/gifs/custom-snippet-editing.gif)

추가를 고려할 만한 항목:

- 프로젝트 파일 구조에 맞는 **컴포넌트 스캐폴드** (예: 표준 임포트와 레이아웃 래퍼를 포함하는 `page` 스니펫).
- **테스트 보일러플레이트** — 항상 필요한 임포트가 포함된 테스트 프레임워크의 `describe`/`it` 구조.
- 프로젝트 고유 이벤트 이름이 미리 입력된 **로깅 또는 텔레메트리 호출**.
- 오류 처리가 포함된 표준 `fetch`/axios/SDK 호출 패턴을 감싼 **API 클라이언트 호출**.

JSON 형식은 간단합니다 — 각 스니펫은 `name`(자동 완성에 표시되는 것)과 `snippet` 본문으로만 구성됩니다. 가져오기 전에 다운로드한 JSON을 텍스트 에디터에서 편집하세요.

## <a name="see-also"></a>참고 항목

- [커스텀 스니펫 참조](./editor-lite#custom-snippets) — 플레이스홀더 구문, 범위 지정, 앱 내 스니펫 관리 방법.
- [시작하기](./editor) — Spck Editor 설치 및 기능 개요.
