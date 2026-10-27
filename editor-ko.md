# <a name="getting-started"></a>시작하기

## <a name="getting-started-overview"></a>개요

Spck Editor는 개발자를 위해 설계된 여러 변형 버전이 있는 모바일 코드 편집 솔루션입니다.

### 버전

#### Spck Editor (무료)

- 기본적인 모바일 코드 편집 기능
- Android·iOS의 네이티브 Git 통합, 브라우저의 isomorphic-git 기반 Git

#### Spck Editor Lite

**가격**: 일회성 결제
**기능**:

- 사용자 지정 스니펫
- 예측 키보드
- 독점 네온 테마
- 향상된 Git 통합

#### Spck for NodeJS

**플랫폼**: Android 전용
**핵심 기능**: NodeJS를 지원하는 통합 터미널

향상된 Git 통합은 활성 Node 구독에 포함되며 터미널 평생 이용권 구매로 영구적으로 사용할 수도 있습니다. 두 방식 모두 로그인이 필요합니다.

#### 브라우저 버전

- 어떤 웹사이트에도 임베드 가능
- 가벼운 코드 편집 인터페이스

[편집기 임베드](./editor-embed)

### 주요 기능

- 모바일 우선 디자인
- [Git 지원 및 제한 사항](./git-support)
- 크로스 플랫폼 호환성
- [스크린 리더 지원(실험적)](./screen-reader-support)

### <a name="git-credentials"></a>Git 자격 증명 및 풀 리퀘스트

<a name="pull-request-management"></a>

[Git 지원](./git-support)에서 [토큰 설정](./git-support#git-credentials), [풀 리퀘스트 관리](./git-support#pull-request-management), [향상된 Git 통합](./git-support#enhanced-git-integration)을 확인하세요.

### 권장 사용

- 이동 중의 코드 편집
- 빠른 프로젝트 수정
- 학습 및 프로토타이핑

## <a name="getting-started-terminology"></a>용어

| 용어             | 설명                                                                                                                |
| ---------------- | ------------------------------------------------------------------------------------------------------------------- |
| 내비게이션 메뉴  | 모바일 기기의 사이드 메뉴에 있는 첫 번째 탭을 의미하며, 이 메뉴는 브라우저 버전이나 태블릿 모드에서는 사용할 수 없습니다 |
| 파일 메뉴        | 사이드 메뉴 또는 사이드바의 _File_ 탭을 의미합니다                                                                  |
| 추가 키보드      | 모바일 기기에는 일반적으로 사용되는 코딩 기호를 빠르게 삽입할 수 있는 추가 키보드가 있습니다                        |
| 터치 키보드      | 일반적으로 화살표 키, Tab 키 등을 포함하는 키 열을 의미합니다                                                       |
| 터치 액션 바     | 모바일/터치 기기에서 텍스트가 선택될 때 커서 위에 나타나는 플로팅 메뉴입니다                                        |
| 터치 커서        | 모바일/터치 기기에서 텍스트가 선택되거나 커서가 활성화될 때 화면에 표시되는 커서                                    |
| 태블릿 모드      | 태블릿과 같은 더 큰 터치 기기에서 켤 수 있는 설정을 의미합니다                                                      |
| ⌘ 키             | 터치 키보드의 이 기호는 Windows의 Ctrl 키 또는 Mac의 Command 키와 동일합니다                                        |
| ⌥ 키             | 터치 키보드의 이 기호는 Windows의 Alt 키 또는 Mac의 Option 키와 동일합니다                                          |

&nbsp;

&nbsp;

# <a name="screen-reader-support"></a>스크린 리더 지원(실험적)

스크린 리더 지원은 **실험적**입니다. [스크린 리더 가이드](./screen-reader-support)에서 활성화, 문서 편집, 키보드 탐색, 제한 및 [피드백](./screen-reader-support#screen-reader-feedback)을 확인하세요.

&nbsp;

&nbsp;

# <a name="keyboard-shortcuts"></a>키보드 단축키

## <a name="keyboard-shortcuts-overview"></a>개요

이 편리한 키보드 단축키로 번개처럼 빠른 효율성을 잠금 해제하세요! 완전한 카탈로그는 아니지만, 이 보석들은 여러분의 생산성을 강화하고 내비게이션을 손쉽게 만들어줄 것입니다.

### 주요 하이라이트

- **포괄적이지 않음**: 가장 실용적인 단축키 모음
- **목적**: 빠르고 직관적인 명령어로 워크플로우 향상
- **이점**: 시간 절약 및 마우스 의존성 감소

> 💡 **프로 팁**: 이 단축키들을 외우고, 생산성이 치솟는 것을 지켜보세요! 🌟

`Settings > Editor > Keyboard Shortcuts`로 이동하여 단축키 전체 목록을 볼 수 있습니다.

> 프리미엄 사용자는 추가 키보드에서 직접 또는 `⌘ K` 단축키를 사용하여 키보드 단축키에 액세스할 수도 있습니다.

> `Settings > Touch > Show ⌘ Key` 및 `Settings > Touch > Show ⌥ Key`를 켜서 Ctrl/Command 키 (⌘)와 Alt/Options 키를 활성화합니다.

키보드 포커스, 메뉴 활성화 및 접근 가능한 문서 편집은 [스크린 리더 지원(실험적)](./screen-reader-support)을 참고하세요.

## <a name="keyboard-shortcuts-editor"></a>편집기

| 단축키 | 작업                                            |
| ------ | ----------------------------------------------- |
| ⌘ A    | 모두 선택                                       |
| ⌘ C    | 복사                                            |
| ⌘ V    | 붙여넣기                                        |
| ⌘ X    | 잘라내기                                        |
| ⌘ Z    | 실행 취소                                       |
| ⌘ ⇧ Z  | 다시 실행                                       |
| ⌘ D    | 줄 복제                                         |
| ⌘ /    | 줄 주석/주석 해제                               |
| ⌥ F    | 코드 포맷                                       |
| ⌘ F    | 찾기                                            |
| ⌘ G    | 다음 찾기 (선택한 텍스트와 함께 작동)           |
| ⌘ ⇧ G  | 이전 찾기                                       |
| ⌘ L    | 줄로 이동                                       |

## <a name="keyboard-shortcuts-quick-actions"></a>빠른 작업

| 단축키 | 작업                                            |
| ------ | ----------------------------------------------- |
| ⌘ ⇧ C  | Git 커밋                                        |
| ⌘ O    | 최근 파일 열기                                  |
| ⌘ ⇧ P  | 프로젝트 미리보기 실행                          |
| ⌘ P    | 파일 미리보기 전환 (SVG, Markdown)              |
| ⌘ K    | **Supporter+**: 단축키 열기                     |

&nbsp;

&nbsp;

# <a name="touch-settings"></a>터치 설정

## <a name="touch-settings-extra"></a>추가 키보드

- 추가 키보드는 터치 기기를 위해 설계된 기호 키보드입니다.
- 추가 키/기호는 키를 길게 눌러 옵션 메뉴를 열어 액세스할 수 있습니다.
- `Settings > Touch > Extra Keyboard` 메뉴에서 활성화 또는 비활성화할 수 있습니다.

> 💡 **프로 팁**: 추가 키보드와 호환되는 텍스트 둘러싸기에 대한 팁은 _**고급 편집**_ 을 참조하세요.

## <a name="touch-settings-touch"></a>터치 키보드

- 터치 키는 화살표 키, Command 키 및 기타 자주 사용되는 키를 포함하는 키 열로 구성됩니다.
- 이 기능은 터치 기기에서 사용할 수 있습니다.
- `Settings > Touch > Touch Keyboard` 섹션에서 켜거나 끌 수 있습니다.

> 💡 **프로 팁**: 설정을 조정하여 이 키보드의 개별 키를 사용자 지정할 수 있습니다.

## <a name="touch-settings-action-bar"></a>터치 액션 바

- 텍스트가 선택되면 복사, 잘라내기 및 붙여넣기 옵션이 있는 액션 바가 표시됩니다.
- 이 기능은 `Settings > Touch > Touch Action Bar`에서 활성화하거나 비활성화할 수 있습니다.

## <a name="touch-settings-cursors"></a>터치 커서

- 텍스트가 선택되거나 커서가 활성화될 때 나타나는 화면 커서.
- 이 기능은 `Settings > Touch > Touch Cursors`에서 활성화하거나 비활성화할 수 있습니다.

> 💡 **프로 팁**: 모바일 기기에 마우스/포인팅 장치가 페어링되어 있지 않은 한 이 기능을 비활성화하는 것은 권장되지 않습니다. 터치 커서를 비활성화하면 편집 시 화면 가시성이 향상되고 외부 포인팅 장치를 사용할 때 편집 경험이 개선될 수 있습니다.

## <a name="touch-settings-predictive"></a>예측 키

- 예측 키는 표준 추가 키보드를 대체하는 프리미엄 기능입니다.
- 일반 추가 키보드에서 길게 누르고 선택해야 하는 대신 원터치 기호 입력을 제공합니다.
- 키는 파일의 특정 위치에 나타나는 기호의 통계적 빈도에 따라 정렬됩니다.
- `Settings > Touch > Predictive Keyboard`에서 켜거나 끌 수 있습니다.

> 💡 **프로 팁**: 예측 키는 일부 사용자가 선호할 수 있는 일반 추가 키보드를 대체합니다. 예측 키는 편집기의 **Lite** 버전에서 기본 옵션이며, 일반 추가 키보드로 되돌리려면 끌 수 있습니다.

&nbsp;

&nbsp;

# <a name="file-navigation"></a>파일 내비게이션

## <a name="file-navigation-overview"></a>개요

- 파일 간 이동에는 여러 가지 방법이 있습니다
- 사이드 메뉴의 파일을 사용하여 파일을 탐색할 수 있습니다
- 빵 부스러기(breadcrumb)를 사용하여 현재 파일 디렉토리에서 시작하여 파일을 탐색할 수 있습니다
- `Ctrl-O`로 최근 파일을 열어 파일을 빠르게 검색할 수 있습니다
- 파일 사이드 메뉴의 "Locate" 아이콘을 사용하여 현재 파일을 빠르게 찾을 수 있습니다
- 소스 제어 및 검색 사이드 메뉴도 파일 간 이동을 위한 독특한 방법을 제공합니다

## <a name="file-navigation-tabs"></a>파일 탭 관리

### 탭 동작

- 파일은 처음 열릴 때 자동으로 고정 해제됩니다
- 편집이 이루어지면 탭이 고정됩니다

### 탭 정렬 옵션

파일은 다음 순서로 정렬할 수 있습니다:

- 알파벳 순서
- 파일 확장자
- 파일 경로

### 대체 내비게이션 채널

- **소스 제어 메뉴**: 버전 관리 컨텍스트를 통해 파일 탐색
- **검색 메뉴**: 검색 기준에 따라 파일 찾기 및 액세스

> 💡 **프로 팁**: 파일 탭은 `Settings > Appearance > Show File Tabs`에서 보기를 끌 수 있습니다. 작은 기기에서 화면 공간을 최대화하려면 _젠 모드_ 를 참조하세요.

&nbsp;

&nbsp;

# <a name="advanced-editing"></a>고급 편집

## 예측 키보드를 효율적으로 사용하기

### 기본 선택

- 두 번 탭하여 단어 또는 텍스트 블록 선택

### 텍스트 둘러싸기

괄호 또는 따옴표 쌍을 사용하여 선택한 텍스트를 빠르게 둘러쌉니다:

- 소괄호: `( )`
- 대괄호: `[ ]`
- 중괄호: `{ }`
- 작은따옴표: `' '`
- 큰따옴표: `" "`

### 내비게이션 및 편집

#### 텍스트 검색

- `⌘ G`: 다음 인스턴스 찾기
- `⌘ ⇧ G`: 이전 인스턴스 찾기

#### 들여쓰기

- 텍스트 블록 선택
- Tab을 눌러 들여쓰기

&nbsp;

## <a name="multiple-cursors"></a>다중 커서

### 빠른 설정

- Alt/Option 키로 다중 커서를 활성화하세요! ✨
- `Settings > Touch > Show ⌥ Key`로 이동하여 활성화

### 사용 방법

1. ⌥ 및 ⌘ 키를 모두 선택
2. 원하는 위치에 정확히 커서를 배치하려면 클릭
3. 여러 줄을 동시에 쉽게 편집! 💻

> 💡 **프로 팁**: 다중 커서 편집 = 번개처럼 빠른 코드 변환! ⚡️
> 명령 팔레트 명령 `Add Cursor Above` 및 `Add Cursor Below`를 사용하여 다중 커서를 추가할 수도 있으며, 이는 현재 커서 위치 바로 위 또는 아래에 커서를 추가합니다.

&nbsp;

&nbsp;

# <a name="enhanced-git-integration"></a>Git 지원

자격 증명, 풀 리퀘스트 관리, 커밋 검사 및 향상된 Git 통합 이용 조건은 [Git 가이드](./git-support)를 참고하세요.

<a name="merge-conflict-resolution"></a>

기본 Git은 diff 뷰어의 **Accept Current**, **Accept Incoming**, **Accept Both**, **Resolve**를 통한 [충돌 해결](./git-support#merge-conflict-resolution)을 포함합니다.

## <a name="git-limitations"></a>Git 제한 사항

<a name="git-limitations-overview"></a>
<a name="git-limitations-memory"></a>
<a name="git-limitations-symlinks"></a>
<a name="git-limitations-cli"></a>

Android·iOS 로컬 프로젝트는 네이티브 libgit2, 브라우저는 isomorphic-git, 원격 프로젝트는 호스트 Git 바이너리를 사용합니다. 저장소 위치, 메모리, 심볼릭 링크, 원격 대안은 [Git 제한 사항](./git-support#git-limitations)을 참고하세요.

&nbsp;

&nbsp;

# <a name="zen-mode"></a>🌟 젠 모드

## 개요

젠 모드는 작은 디스플레이에서 코딩 경험을 변화시키도록 설계된 즐겁고 공간을 최대화하는 편집기 구성입니다.

젠 모드는 다음으로 구성됩니다:

- 설정에서 `Show Line Numbers` 끄기
- `Show File Tab` 끄기
- `Touch Action Bar` 끄기

### 주요 기능

#### 🧘‍♀️ 극대화된 화면 공간

- **줄 번호여, 안녕!**
  - 소중한 가로 공간 확보
  - 텍스트가 비좁아 보이는 것 방지
  - 깨끗하고 미니멀한 모습 채택

#### 🎨 간소화된 인터페이스

- **액션 바 최소화**
  - 어수선한 도구 모음과 작별
  - 대체 입력 방법 활용:
    - 추가 키보드 붙여넣기/잘라내기 버튼
    - 키보드 단축키 (`Ctrl-C/Ctrl-V`)

#### 📂 단순화된 내비게이션

- **파일 탭 제거**
  - `Ctrl-O`가 여러분의 새로운 내비게이션 베스트 프렌드가 됩니다
  - 더 깔끔한 작업 공간
  - 더 빠른 컨텍스트 전환

> 💡 **프로 팁**: 모든 사람의 코딩 스타일은 다릅니다! 젠 모드를 실험하여 여러분의 워크플로우와 공명하는지 확인해 보시기를 권장합니다. 완벽한 코딩 환경은 몇 번의 토글만 누르면 됩니다! 🌈✨
