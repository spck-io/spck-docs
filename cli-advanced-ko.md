# <a name="cli-advanced-usage"></a>CLI 고급 사용법

## <a name="cli-commands"></a>CLI 명령

### 기본 명령

```bash
# CLI 시작
spck

# 설정 마법사 실행
spck --setup

# 계정 정보 표시
spck --account

# 로그아웃 및 자격 증명 삭제
spck --logout

# 도움말 표시
spck --help

# 버전 표시
spck --version
```

### 고급 옵션

```bash
# 커스텀 구성 파일 사용
spck --config /path/to/config.json
spck -c /path/to/config.json

# 루트 디렉터리 재정의
spck --root /path/to/project
spck -r /path/to/project

# 릴레이 서버 재정의 (예: 특정 리전 사용)
spck --server cli-eu-1.spck.io
spck -s cli-na-1.spck.io
```

## <a name="ai-coding-agents"></a>AI 코딩 에이전트 (ACP)

Spck CLI는 [Agent Client Protocol (ACP)](https://agentclientprotocol.com/)을 통해 Spck Editor의 AI 채팅을 로컬에 설치된 AI 코딩 에이전트(**Claude Code**, **Codex** 또는 **Gemini CLI**)에 연결합니다. 모델은 본인의 구독으로 본인의 머신에서 실행되며, 디스크의 실제 파일을 편집하고, 권한 프롬프트를 휴대폰으로 전달합니다.

![Spck Editor의 AI 채팅에서 로컬 AI 모드가 휴대폰으로 Claude Code를 구동하는 모습](https://docs.spck.io/assets/gifs/acp-ai.gif)

→ **[모바일에서 AI 코딩 에이전트 (ACP)](./cli-acp)** — 전체 가이드: 지원되는 에이전트, 설치, 결제 및 속도 제한(Anthropic이 타사 클라이언트에 적용하는 별도 Claude Code 할당량 포함), 구성, FAQ, 문제 해결.

> 💡 **팁**: **tmux**를 사용하면 연결을 끊은 후에도 AI 에이전트 세션이 계속 실행됩니다. 데스크톱에서 tmux 세션을 시작하고(`tmux new -s code`), 에이전트를 실행한 다음, 휴대폰의 Spck CLI 터미널에서 다시 연결하세요(`tmux attach -t code`). 일반 셸 에이전트와 ACP 모드 에이전트 모두에서 작동합니다. 영구적인 원격 서버 설정을 포함한 전체 가이드는 [Tmux 사용하기](./tmux)를 참조하세요.

## <a name="advanced-usage"></a>고급 사용법

### 다중 프로젝트

서로 다른 프로젝트에 대해 별도의 CLI 인스턴스를 동시에 실행:

```bash
# 터미널 1: 프로젝트 A
cd /path/to/projectA
spck

# 터미널 2: 프로젝트 B
cd /path/to/projectB
spck
```

각 프로젝트는 고유한 구성과 연결을 유지합니다.

> 💡 **팁**: 여러 CLI 인스턴스를 사용하여 데스크톱과 스마트폰 간에 파일을 전송할 수도 있습니다. 단계별 가이드는 [모바일과 데스크톱 간 파일 전송](./cli-file-transfer)을 참조하세요.

### 커스텀 구성 파일

시나리오별로 특화된 구성 파일 만들기:

```bash
# 개발 구성
spck --config ~/configs/dev-config.json

# 프로덕션 구성 (읽기 전용, 터미널 없음)
spck --config ~/configs/prod-config.json
```

### 환경별 설정

**로컬 개발:**

```json
{
  "security": {
    "userAuthenticationEnabled": false
  },
  "terminal": {
    "enabled": true
  }
}
```

**프로덕션 서버:**

```json
{
  "security": {
    "userAuthenticationEnabled": true
  },
  "terminal": {
    "enabled": false
  }
}
```

### 높은 CPU 사용량

무시 패턴을 추가하여 파일 감시 줄이기:

```json
{
  "filesystem": {
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/dist/**",
      "**/build/**",
      "**/.next/**",
      "**/coverage/**",
      "**/.cache/**"
    ]
  }
}
```

동시 터미널 수 제한:

```json
{
  "terminal": {
    "maxTerminals": 5
  }
}
```

## <a name="mobile-prompt"></a>모바일용 셸 프롬프트 줄이기

모바일 기기는 가로 화면 공간이 제한적입니다. 기본 셸 프롬프트(일반적으로 현재 디렉터리 경로, 사용자 이름, 호스트명 포함)는 터미널을 복잡하게 만들어 명령 출력을 읽기 어렵게 합니다.

프롬프트를 `$ `만으로 변경하면 작은 화면에서 훨씬 깔끔한 터미널 경험을 얻을 수 있습니다.

### Bash

`~/.bashrc`에 다음을 추가:

```bash
export PS1='\$ '
```

셸을 재시작하지 않고 적용:

```bash
source ~/.bashrc
```

### Zsh

`~/.zshrc`에 다음을 추가:

```zsh
PROMPT='$ '
```

셸을 재시작하지 않고 적용:

```zsh
source ~/.zshrc
```

### PowerShell (Windows)

프로파일 파일이 없으면 생성한 후 열기:

```powershell
New-Item -Path $PROFILE -Type File -Force
notepad $PROFILE
```

프로파일에 다음을 추가:

```powershell
function prompt { "$ " }
```

셸을 재시작하지 않고 적용:

```powershell
. $PROFILE
```

### 명령 프롬프트 (Windows)

현재 세션에 대한 최소 프롬프트 설정:

```cmd
PROMPT $$
```

영구적으로 적용하려면 **제어판 → 시스템 → 고급 시스템 설정 → 환경 변수**에서 `PROMPT`를 값 `$$`로 **사용자** 또는 **시스템** 환경 변수로 추가하세요.
