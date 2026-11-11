# <a name="getting-started"></a>Spck CLI 시작하기

## <a name="overview"></a>개요

Spck CLI가 정식 출시되었습니다. 휴대폰이나 태블릿의 Spck Editor를 컴퓨터에 연결하여 파일 편집, Git, 터미널, 로컬 서버 미리보기를 이용하세요. 암호화된 릴레이 또는 직접 [Fast Lane](./cli#fast-lane) 연결(Supporter 및 Gold)을 사용합니다.

## <a name="requirements"></a>요구 사항

Lite는 Spck CLI를 통해 데스크톱이나 공개 VM에 있는 프로젝트를 편집할 수 있습니다. 원격 프로젝트에는 Lite 일회성 구매와 별도로 **Spck 계정과 활성 Spck 구독**이 필요합니다. 구독은 Spck 서버의 지속적인 호스팅, 운영 및 유지 관리 비용을 지원합니다. 포함된 로컬 편집 및 Git 도구는 구독 없이 계속 사용할 수 있습니다.

### 필수

- **Node.js**: **22.22.2+ (22.x), 24.15.0+ (24.x), 또는 26.0.0+** (`^22.22.2 || ^24.15.0 || >=26.0.0`).
- **Spck Editor 계정**: 무료 계정(30분/일) 또는 프리미엄 구독(무제한)
- **Spck Editor 모바일 앱**: [Android](https://play.google.com/store/apps/details?id=io.spck) 또는 [iOS](https://apps.apple.com/us/app/spck-editor/id1507309511)

### 선택 사항 (권장)

- **Git**: 원격 프로젝트의 [Git 통합](./git-support#git-limitations-cli)에 2.20.0 이상 필요
- **ripgrep**: 15.0.0 이상(파일 검색 속도가 100배 향상)

## <a name="installation"></a>설치

### 옵션 1: npx로 실행 (설치 불필요)

```bash
npx spck@latest
```

최신 CLI 버전을 요청하므로 처음 설정하거나 가끔 사용할 때 좋습니다. `npx spck`는 설치된 버전을 재사용할 수 있습니다.

### 옵션 2: 전역 설치

```bash
npm install -g spck
spck
```

한 번 설치한 뒤 매일 `spck`로 실행하세요. 업데이트는 `npm install -g spck@latest`를 사용합니다. 원격 연결에는 계속 인터넷이 필요합니다.

## <a name="demo"></a>데모

새로운 Fast Lane 기능이 포함된 [Spck CLI 동영상 보기](https://youtu.be/EtfEhd5EmKM).

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

브라우저가 localhost에 접근하지 못하면 릴레이를 통해 로그인합니다. CLI의 로그인 QR 코드나 링크를 사용하면 다른 기기에서도 로그인할 수 있습니다. 이 코드는 프로젝트 연결 QR 코드와 다릅니다.

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

새 프로젝트는 첫 에디터 연결이 성공할 때까지 연결 QR 코드를 표시합니다. 이후 실행에서는 대시보드가 바로 열립니다. **`c`**로 QR 코드와 연결 정보를 다시 표시하고, **`l`**로 로그를 확인하세요. QR 코드가 맞지 않으면 터미널을 크게 하세요.

### 방법 1: QR 코드 (권장)

1. Spck Editor 열기 → **프로젝트** → **새 프로젝트** → **원격 서버 연결**
2. QR 코드 아이콘 탭
3. 터미널에 표시된 QR 코드를 스캔합니다. 앱이 자동으로 연결됩니다.

> 💡 **참고**: 기기의 카메라 앱으로 코드를 스캔할 수도 있습니다. 앱이 설치되어 있으면 링크가 Spck Editor에서 열립니다.

### 방법 2: 수동 입력

QR 코드를 스캔할 수 없는 경우:

1. Spck Editor 열기 → **프로젝트** → **새 프로젝트** → **원격 서버 연결**
2. 터미널에 표시된 **클라이언트 ID**와 **시크릿** 입력
3. 터미널에 표시된 릴레이 서버 선택
4. **연결** 탭

**Require PIN to connect**가 켜져 있으면 CLI 대시보드에서 설정한 PIN을 입력하세요. 앱은 PIN을 저장하지 않습니다. [연결 PIN](./cli-config#connection-pin)을 참고하세요.

## <a name="next-steps"></a>다음 단계

1. **릴레이 시스템 이해하기**: CLI의 트래픽 라우팅 방식과 서버 선택 방법을 알아보세요 — [CLI 레퍼런스](./cli) 참조
2. **설정 구성하기**: 터미널, 보안, 파일시스템 설정 조정 — [구성](./cli-config) 참조
3. **고급 기능 살펴보기**: CLI 명령, AI 코딩 에이전트, 다중 프로젝트 — [고급 사용법](./cli-advanced) 참조
4. **기기 간 파일 전송하기**: 스마트폰과 데스크톱 간에 프로젝트를 무선으로 복사 — [파일 전송](./cli-file-transfer) 참조
5. **세션 유지하기**: tmux로 기기 간 세션 공유 — [Tmux 사용하기](./tmux) 참조
