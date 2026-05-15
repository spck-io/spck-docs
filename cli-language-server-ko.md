# <a name="cli-language-server"></a>CLI Language Server

## <a name="cli-ls-overview"></a>개요

Spck CLI에는 TypeScript, JavaScript, Python, HTML, CSS, SCSS 언어 서버를 원격 호스트에서 직접 실행하는 완전한 Language Server Protocol (LSP) 브리지가 포함되어 있습니다. CLI 세션에 연결되면 Spck Editor는 모바일 내장 언어 서버 대신 자동으로 원격 언어 서버를 사용합니다.

> 💡 **팁**: CLI 없이 사용할 수 있는 내장 언어 서버에 대한 설명은 [에디터 Language Server](./editor-language-server)를 참조하세요.

## <a name="cli-ls-architecture"></a>아키텍처

CLI 언어 서버는 프로젝트 파일과 동일한 머신에서 실행됩니다. 이는 모바일에서 사용되는 브라우저 기반 방식에 비해 여러 가지 중요한 이점을 제공합니다.

### 파일 전송 불필요

내장 모바일 언어 서버는 파일을 분석하기 전에 디바이스로 전송하여 브라우저 워커에 로드해야 합니다. CLI를 사용하면 언어 서버가 디스크에서 직접 파일을 읽으므로 전송이 필요하지 않습니다. 이를 통해 대역폭 오버헤드가 제거되고 대규모 프로젝트에서도 분석 속도가 빠르게 유지됩니다.

### 전체 프로젝트 인식

CLI 언어 서버는 다음을 포함한 전체 프로젝트 디렉터리에 접근할 수 있습니다.

- 모든 하위 디렉터리의 모든 소스 파일
- 서드파티 타입 해석을 위한 `node_modules/`
- 모든 깊이에서 자동으로 검색되는 `tsconfig.json` 파일
- `.js`, `.ts`, `.d.ts`, `.jsx`, `.tsx`, `.vue` 및 관련 선언 파일

즉, 에디터에서 해당 파일을 열지 않은 경우에도 파일 경계를 넘어 정의로 이동, 참조 찾기, 심볼 이름 바꾸기가 올바르게 작동합니다.

### 올바른 `tsconfig.json` 처리

TypeScript 언어 서버는 프로젝트의 `tsconfig.json`(또는 `jsconfig.json`)을 자동으로 검색하고 준수합니다. 경로 별칭(`paths`), 컴파일러 옵션(`strict`, `target`, `lib`), 프로젝트 참조, 모노레포 워크스페이스 레이아웃이 모두 올바르게 처리됩니다. 모바일 내장 언어 서버는 시작 시 파일 시스템에 접근할 수 없기 때문에 `tsconfig.json`을 읽을 수 없습니다.

### 지속적인 프로세스

언어 서버 프로세스는 CLI 세션이 진행되는 동안 계속 실행됩니다. 프로젝트의 인메모리 인덱스를 빌드하고 편집 간에 이를 유지하므로 초기 시작 이후에도 응답이 빠르게 유지됩니다.

## <a name="cli-ls-features"></a>지원되는 기능

| 기능 | 설명 |
| --- | --- |
| **코드 완성** | 타입 시그니처와 함께 관련성 순으로 정렬된 컨텍스트 인식 제안 |
| **호버 정보** | 커서 아래 심볼의 타입 정보 및 JSDoc 문서 |
| **시그니처 도움말** | 함수 호출 입력 시 매개변수 힌트 및 문서 |
| **정의로 이동** | `node_modules`의 심볼을 포함한 모든 심볼의 선언으로 이동 |
| **참조 찾기** | 프로젝트 전체에서 심볼의 모든 사용처 목록 |
| **심볼 이름 바꾸기** | 심볼 이름을 바꾸고 모든 참조를 원자적으로 업데이트 |
| **진단** | 입력 중 실시간 오류 및 경고 강조 표시 |
| **Markdown 렌더링** | 구문 강조 코드 블록이 포함된 Markdown으로 렌더링된 호버 및 시그니처 문서 |

## <a name="cli-ls-languages"></a>지원되는 언어

| 언어 | 완성 | 호버 | 시그니처 | 진단 |
| --- | --- | --- | --- | --- |
| TypeScript / TSX | ✓ | ✓ | ✓ | ✓ |
| JavaScript / JSX | ✓ | ✓ | ✓ | ✓ |
| Python | ✓ | ✓ | ✓ | ✓ |
| HTML | ✓ | ✓ | — | ✓ |
| CSS / SCSS / Less | ✓ | ✓ | — | ✓ |

## <a name="cli-ls-config"></a>설정

언어 서버 지원은 기본적으로 활성화되어 있습니다. 설정 파일에서 제어할 수 있습니다.

```json
{
  "languageServer": {
    "enabled": true,
    "typescript": {
      "enabled": true
    },
    "python": {
      "enabled": true
    }
  }
}
```

- **`languageServer.enabled`** (boolean): 모든 원격 언어 서버의 마스터 스위치. 기본값: `true`.
- **`languageServer.typescript.enabled`** (boolean): TypeScript/JavaScript 언어 서버 활성화. 기본값: `true`.
- **`languageServer.python.enabled`** (boolean): Python 언어 서버 활성화 (`PATH`에 `pylsp` 필요). 기본값: `true`.

## <a name="cli-ls-requirements"></a>요구 사항

- **TypeScript / JavaScript**: CLI에 포함되어 있습니다. 추가 설치 불필요.
- **Python**: [`python-lsp-server`](https://github.com/python-lsp/python-lsp-server) 필요 (`pip install python-lsp-server`).
- **HTML / CSS / SCSS**: CLI에 포함되어 있습니다. 추가 설치 불필요.

## <a name="cli-ls-vs-mobile"></a>CLI vs. 모바일 언어 서버

| 기능 | CLI Language Server | 모바일 내장 |
| --- | --- | --- |
| 전체 프로젝트 파일 접근 | ✓ | — |
| `tsconfig.json` / `jsconfig.json` | ✓ | — |
| `node_modules` 타입 해석 | ✓ | — |
| 파일 간 정의로 이동 | ✓ | 제한적 |
| 파일 간 참조 찾기 | ✓ | — |
| 심볼 이름 바꾸기 | ✓ | — |
| Python 지원 | ✓ | — |
| 오프라인 동작 (CLI 없음) | — | ✓ |

&nbsp;

&nbsp;
