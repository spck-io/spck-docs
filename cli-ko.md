# <a name="cli-reference"></a>CLI 참조

## <a name="key-features"></a>주요 기능

- **원격 파일시스템**: Spck Editor 모바일 앱에서 로컬 파일 접근 및 편집
- **Git 통합**: 전체 git 작업 (커밋, 푸시, 풀, 브랜치 관리) — Git 2.20.0 이상 필요
- **터미널 접근**: xterm.js를 사용한 인터랙티브 터미널 세션
- **브라우저 프록시**: Spck Editor 내에서 전체 화면 브라우저 뷰로 로컬 서버 미리보기
- **빠른 검색**: ripgrep 자동 감지를 통한 최적화된 파일 검색 (설치 시 100배 빠름)
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

동시 CLI 연결의 최대 수와 일일 사용 제한은 계정 유형에 따라 다릅니다:

| 플랜 | CLI 연결 수 | 일일 제한 |
| --------- | --------------- | ----------- |
| 무료 | 1 | 30분 |
| 지원자 | 2 | 무제한 |
| 골드 | 5 | 무제한 |

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
