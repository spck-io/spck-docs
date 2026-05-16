# <a name="getting-started"></a>Spck CLI 시작하기

## <a name="overview"></a>개요

Spck CLI는 안전한 WebSocket 연결을 통해 로컬 개발 환경을 Spck Editor 모바일 앱에 연결하는 커맨드라인 도구입니다. 실행한 후에는 스마트폰이나 태블릿에서 로컬 파일을 탐색하고 편집하거나, 터미널 명령을 실행하거나, 로컬 서버를 미리볼 수 있습니다.

## <a name="requirements"></a>요구 사항

### 필수

- **Node.js**: 18.0.0 이상
- **Spck Editor 계정**: 무료 계정(30분/일) 또는 프리미엄 구독(무제한)
- **Spck Editor 모바일 앱**: [Android](https://play.google.com/store/apps/details?id=io.spck) 또는 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 선택 사항 (권장)

- **Git**: 2.20.0 이상(Git 연동 기능에 필요)
- **ripgrep**: 15.0.0 이상(파일 검색 속도가 100배 향상)

## <a name="installation"></a>설치

### 옵션 1: npx로 실행 (설치 불필요)

```bash
npx spck
```

항상 최신 버전을 사용합니다. 처음 설정하거나 가끔 사용할 때 적합합니다.

### 옵션 2: 전역 설치

```bash
npm install -g spck
spck
```

시작 속도가 빠르고, 오프라인에서도 동작하며, 매일 사용하기에 편리합니다.

## <a name="demo"></a>데모

Spck CLI를 모바일 앱에 연결하고 로컬 파일을 원격으로 편집하는 짧은 데모입니다:

![Remote Project features in Spck Editor](https://docs.spck.io/assets/gifs/remote-cli-preview.gif)

## <a name="first-time-setup"></a>최초 설정

CLI를 처음 실행하면 인터랙티브 설정 마법사가 다음 단계를 안내합니다.

### 1. 인증

```bash
spck
# ENTER를 눌러 브라우저 열기
# Spck Editor 계정으로 로그인
# CLI 권한 부여
# 터미널로 돌아오기
```

자격 증명은 `~/.spck-editor/.credentials.json`에 저장되며 세션 간에 유지됩니다.

### 2. 프로젝트 구성

마법사가 다음을 구성합니다.

- **루트 디렉터리**: 파일 접근의 기본 디렉터리(기본값: 현재 디렉터리)
- **프로젝트 이름**: 모바일 앱에 표시되는 이름(기본값: 디렉터리 이름)

### 3. Git 연동 (선택 사항)

`.gitignore` 파일이 감지되면 CLI가 `.spck-editor/`를 추가하여 시크릿이 실수로 커밋되지 않도록 제안합니다.

```
Add .spck-editor/ to .gitignore? (Y/n)
```

**권장**: 연결 자격 증명을 보호하려면 `Y`를 선택하세요.

### 설정 재실행

언제든지 재구성하려면:

```bash
spck --setup
```

## <a name="connecting"></a>Spck Editor 연결

CLI가 실행되면 QR 코드와 연결 정보가 표시됩니다.

### 방법 1: QR 코드 (권장)

**중요**: QR 코드를 스캔하기 **전에** Spck Editor 앱을 설치하세요.

**Android:**

1. 카메라 앱 또는 빠른 설정의 QR 스캐너 사용
2. 감지되면 알림을 탭하여 Spck Editor 열기
3. 앱이 자동으로 연결됨

> 💡 **참고**: 일부 QR 코드 스캐너는 Spck Editor를 직접 여는 커스텀 스킴을 처리하지 못할 수 있습니다. URL을 복사하여 Chrome에 붙여넣으면 Spck Editor가 실행됩니다.

**iOS:**

1. 카메라 앱 또는 제어 센터의 QR 스캐너 사용
2. 감지되면 알림을 탭하여 Spck Editor 열기
3. 앱이 자동으로 연결됨

> 💡 **참고**: Spck Editor에는 내장 QR 스캐너가 없습니다. 기기의 기본 QR 기능을 사용하세요.

### 방법 2: 수동 입력

QR 코드가 작동하지 않는 경우:

1. Spck Editor 열기 → **프로젝트** → **새 프로젝트** → **원격 서버 연결**
2. 터미널에 표시된 **클라이언트 ID**와 **시크릿** 입력
3. **연결** 탭

## <a name="next-steps"></a>다음 단계

1. **릴레이 시스템 이해하기**: CLI의 트래픽 라우팅 방식과 서버 선택 방법을 알아보세요 — [CLI 레퍼런스](./cli) 참조
2. **설정 구성하기**: 터미널, 보안, 파일시스템 설정 조정 — [구성](./cli-config) 참조
3. **고급 기능 살펴보기**: CLI 명령, AI 코딩 에이전트, 다중 프로젝트 — [고급 사용법](./cli-advanced) 참조
4. **기기 간 파일 전송하기**: 스마트폰과 데스크톱 간에 프로젝트를 무선으로 복사 — [파일 전송](./cli-file-transfer) 참조
5. **세션 유지하기**: tmux로 기기 간 세션 공유 — [Tmux 사용하기](./tmux) 참조
