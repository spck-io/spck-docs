# <a name="cli-reference"></a>CLI 참조

## <a name="key-features"></a>주요 기능

- **원격 파일시스템**: Spck Editor 모바일 앱에서 로컬 파일 접근 및 편집
- **Git 통합**: 전체 git 작업 (커밋, 푸시, 풀, 브랜치 관리) — Git 2.20.0 이상 필요
- **터미널 접근**: xterm.js를 사용한 인터랙티브 터미널 세션
- **브라우저 프록시**: Spck Editor 내에서 전체 화면 브라우저 뷰로 로컬 서버 미리보기
- **빠른 검색**: ripgrep 자동 감지를 통한 최적화된 파일 검색 (설치 시 100배 빠름)
- **로컬 AI 코딩 에이전트 (ACP)**: Spck Editor의 AI 채팅에서 [Agent Client Protocol](https://agentclientprotocol.com/)을 통해 Claude Code, Codex 또는 Gemini CLI를 제어합니다. 에이전트는 본인의 구독으로 본인의 머신에서 실행됩니다. [모바일에서 AI 코딩 에이전트 (ACP)](./cli-acp) 참조.
- **Fast Lane** (Supporter & Gold): Spck Editor와 CLI 간의 직접 P2P WebRTC 연결로, 릴레이보다 평균 2배 빠릅니다. [Fast Lane](#fast-lane)을 참조하세요.
- **보안**: 선택적 Firebase 인증을 통한 암호화 서명 요청

## <a name="relay-server"></a>릴레이 서버

CLI는 두 장치 간 메시지를 전달하는 릴레이 서버를 통해 Spck Editor에 연결됩니다. 처음 실행할 때 CLI는 지연 시간이 가장 낮은 릴레이 서버를 자동으로 선택하고 설정을 `~/.spck-editor/.credentials.json`에 저장합니다.

**중요**: CLI와 Spck Editor 클라이언트 모두 동일한 릴레이 서버를 사용해야 연결됩니다. 클라이언트가 CLI를 찾을 수 없다면 양쪽이 동일한 릴레이 서버를 선택했는지 확인하세요.

### 사용 가능한 릴레이 서버

| 지역 | URL |
| ------------- | ------------------- |
| 유럽 | `cli-eu-1.spck.io`  |
| 북미 | `cli-na-1.spck.io`  |
| 남아시아 | `cli-sas-1.spck.io` |
| 동아시아 | `cli-ea-1.spck.io`  |

### 릴레이 서버 재정의

```bash
# Use a specific relay server
spck --server cli-eu-1.spck.io

# Short form
spck -s cli-na-1.spck.io
```

재정의는 저장되어 이후 실행 시 재사용됩니다. 자동 선택을 다시 실행하려면 자격 증명을 지우고 재시작하세요:

```bash
spck --logout
spck
```

### Spck Editor에서 릴레이 서버 선택

**Link Remote Server**를 통해 모바일 앱에서 연결할 때 CLI가 사용 중인 것과 동일한 릴레이 서버를 **Relay Server** 드롭다운에서 선택하세요. 릴레이 서버 이름은 연결 후 CLI 출력에 표시됩니다.

## <a name="fast-lane"></a>Fast Lane

Fast Lane은 **Supporter** 및 **Gold** 구독자를 위한 프리미엄 기능입니다. 모든 메시지를 릴레이 서버를 거쳐 보내는 대신, Spck Editor가 WebRTC(P2P)를 사용해 **CLI에 직접 연결**합니다. 릴레이를 거치는 단계가 사라지고 왕복 횟수가 줄어들어 Fast Lane은 **릴레이보다 평균 2배 빠르며**, 파일 작업, 검색, Git, 터미널 입력이 눈에 띄게 빠르게 반응합니다.

릴레이 서버는 여전히 필요합니다. CLI가 등록되는 곳이자 에디터와 CLI 간의 초기 핸드셰이크를 중개하기 때문입니다. 직접 경로가 만들어지면 프로젝트 데이터는 릴레이 대신 그 경로로 전달됩니다.

### 요구 사항

- CLI에 로그인한 계정의 활성 **Supporter** 또는 **Gold** 구독
- Spck CLI **0.7.0 이상** (`npm i -g spck`)
- Spck Editor를 실행하는 기기와 CLI를 실행하는 컴퓨터 모두에서 WebRTC 지원

### Fast Lane 켜기 또는 끄기

**Spck Editor에서:** **Link Remote Server**를 열거나(또는 메뉴에서 기존 연결을 편집하고) **⚡ Fast Lane** 토글을 사용하세요. Supporter 및 Gold 계정의 새 연결에서는 기본적으로 켜져 있습니다.

**CLI에서:** Fast Lane은 기본적으로 활성화되어 있습니다. CLI 대시보드에서 **`f`**를 눌러 현재 프로젝트에 대해 켜거나 끄거나, [프로젝트 구성](./cli-config#fast-lane-settings)에서 `fastLane.enabled`를 설정하세요. 변경 사항은 CLI를 다시 시작한 후 적용됩니다. P2P 트래픽을 차단하는 네트워크에서는 끄세요.

CLI 대시보드에는 현재 Fast Lane 상태(활성, 사용 가능, 꺼짐, 이 플랫폼에서 사용할 수 없음)가 표시되며, Spck Editor의 파일 패널에는 사용 중인 전송 방식과 현재 핑이 `Fast Lane · 24 ms` 또는 `Relay · 80 ms`처럼 표시됩니다.

### 자동 폴백

직접 연결을 만들 수 없는 경우 Spck Editor는 작업을 계속할 수 있도록 자동으로 릴레이로 전환하고 그 이유를 알려 줍니다. 일반적인 이유:

- CLI가 오래됨 — `npm i -g spck`로 업데이트하세요
- CLI 프로젝트 구성에서 Fast Lane이 꺼져 있음
- CLI를 실행하는 컴퓨터 또는 사용 중인 기기에서 WebRTC를 사용할 수 없음
- 릴레이 서버가 아직 Fast Lane을 지원하지 않음
- 네트워크가 직접 P2P 경로를 차단함 (예: 엄격한 기업 방화벽 또는 NAT)

### 보안

Fast Lane 트래픽은 WebRTC(DTLS)로 종단 간 암호화됩니다. 또한 CLI의 인증 핸드셰이크는 해당 DTLS 세션에 묶여 있어, 프로젝트 데이터를 주고받기 전에 CLI가 바로 그 채널에서 연결 비밀 키를 가지고 있음을 증명해야 합니다. 모든 요청은 릴레이와 마찬가지로 암호학적으로 서명됩니다. [CLI 보안](./cli-config#security)을 참조하세요.

## <a name="daily-workflow"></a>일상적인 워크플로우

### 세션 시작

```bash
cd /path/to/project
spck
# Connect from mobile app (auto-connects to saved server)
# Start coding
```

### 파일 편집

1. 모바일 앱에서 파일 탐색
2. 탭하여 열고 편집
3. 파일이 컴퓨터에 자동으로 저장됩니다.

### Git 명령 실행

**옵션 1 - 모바일 앱 GUI:**

- Git 패널 열기
- 변경 사항 확인, 파일 스테이징
- 커밋 및 푸시

**옵션 2 - 터미널:**

```bash
git status
git add .
git commit -m "Update feature"
git push
```

### 터미널 세션

모바일 앱의 터미널 아이콘을 탭하면 사용자 권한으로 전체 셸에 접근할 수 있습니다.

### 세션 종료

```bash
# Keep CLI running for quick reconnects (recommended)
# Or stop with Ctrl+C
```

## <a name="troubleshooting"></a>문제 해결

### 루트 디렉터리를 찾을 수 없음

```bash
# Reconfigure with correct path
spck --setup

# Or specify directly
spck --root /correct/path/to/project
```

### 손상된 구성

```bash
# Clear settings and start fresh
spck --logout
spck --setup
```

### 연결 문제

1. 인터넷 연결 확인
2. CLI와 Spck Editor 모두 **동일한 릴레이 서버**를 사용하는지 확인 (연결 후 CLI 출력에 표시)
3. 로그아웃 후 재연결 시도:
   ```bash
   spck --logout
   spck
   ```
4. 방화벽 설정 확인 — WebSocket 연결 (포트 443)이 허용되어 있는지 확인
5. Fast Lane을 사용할 수 없어 릴레이를 사용 중이라는 알림이 표시되어도 연결은 릴레이를 통해 계속 작동합니다. 원인과 해결 방법은 [Fast Lane](#fast-lane)의 "자동 폴백"을 참조하세요

### QR 코드 스캔 불가

- 스캔 전에 Spck Editor 앱이 설치되어 있는지 확인
- 수동 입력 사용: Projects → New Project → Link Remote Server
- 서드파티 스캐너가 아닌 기본 카메라 앱 사용

### Git 작업이 작동하지 않음

1. Git이 설치되어 있는지 확인:

   ```bash
   git --version  # Requires 2.20.0+
   ```

2. 필요한 경우 설치:

   ```bash
   # macOS
   brew install git

   # Ubuntu/Debian
   sudo apt-get install git

   # Windows: Download from git-scm.com
   ```

### 검색 성능이 느림

100배 빠른 검색을 위해 ripgrep을 설치하세요:

```bash
# macOS
brew install ripgrep

# Ubuntu/Debian
sudo apt-get install ripgrep

# Windows (Chocolatey)
choco install ripgrep

# CLI automatically detects and uses ripgrep
```

### 권한 거부됨

```bash
# View permissions
ls -la /path/to/file

# Fix if needed
chmod 644 /path/to/file

# Don't use sudo - CLI should run as the user who owns the files
```

## <a name="connection-limits"></a>연결 제한

Lite는 Spck CLI를 통해 데스크톱이나 공개 VM에 있는 프로젝트를 편집할 수 있습니다. 원격 프로젝트에는 Lite 일회성 구매와 별도로 **Spck 계정과 활성 Spck 구독**이 필요합니다. 구독은 Spck 서버의 지속적인 호스팅, 운영 및 유지 관리 비용을 지원합니다. 포함된 로컬 편집 및 Git 도구는 구독 없이 계속 사용할 수 있습니다.

동시 CLI 연결의 최대 수와 일일 사용 제한은 계정 유형에 따라 다릅니다:

| 플랜 | CLI 연결 수 | 일일 제한 | Fast Lane |
| --------- | --------------- | ----------- | --------- |
| 무료 | 1 | 30분 | —         |
| 지원자 | 2 | 무제한 | ✓         |
| 골드 | 5 | 무제한 | ✓         |

무료 티어 사용량은 매일 UTC 오전 12:00에 초기화됩니다.

연결 제한에 도달하면:

```
⚠️  Maximum of X CLI connections reached.
Close other CLI instances and try again.
```

일일 무료 티어 제한에 도달하면:

```
⚠️  Daily free tier limit of 30 minutes has been reached.
Upgrade to continue using CLI.
```

활성 연결 확인:

```bash
spck --account
```

> 💡 **참고**: 한 번에 하나의 모바일 기기만 CLI 인스턴스에 연결할 수 있습니다. 각 CLI 인스턴스는 하나의 연결 슬롯을 사용합니다.

## <a name="support"></a>지원

- **웹사이트**: [https://spck.io](https://spck.io)
- **지원**: Spck Editor 모바일 앱을 통해 문의
