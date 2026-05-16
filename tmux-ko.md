# <a name="tmux"></a>Spck CLI와 Tmux 사용하기

Tmux(터미널 멀티플렉서)를 사용하면 터미널 세션을 시작한 창이나 SSH 연결과 독립적으로 실행할 수 있습니다. Spck CLI 사용자에게는 재연결 시에도 세션을 유지하고, 실행 중인 에이전트 세션을 데스크톱과 모바일 간에 공유하며, SSH 연결이 끊어진 후에도 원격 서버에서 CLI를 지속적으로 실행할 수 있음을 의미합니다.

## <a name="installation"></a>설치

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="mac">macOS</button>
    <button type="button" class="ptabs-btn" data-tab="linux">Linux</button>
    <button type="button" class="ptabs-btn" data-tab="windows">Windows (WSL)</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="mac">

```bash
brew install tmux
```

</div>
    <div class="ptabs-pane" data-tab="linux">

**Ubuntu / Debian**

```bash
sudo apt-get install tmux
```

**Fedora / RHEL**

```bash
sudo dnf install tmux
```

**Arch Linux**

```bash
sudo pacman -S tmux
```

</div>
    <div class="ptabs-pane" data-tab="windows">

Tmux는 Linux에서 기본으로 실행됩니다. Windows에서는 [Linux용 Windows 하위 시스템(WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)을 사용한 다음 WSL 내에 tmux를 설치하세요.

**1단계 — WSL 설치(관리자 권한 PowerShell):**

```powershell
wsl --install
```

**2단계 — WSL 터미널을 열고 tmux 설치:**

```bash
sudo apt-get install tmux
```

</div>
  </div>
</div>

## <a name="use-case-1-sharing-agent-sessions-across-desktop-and-mobile"></a>사용 사례 1: 데스크톱과 모바일 간 에이전트 세션 공유

Spck CLI와 tmux를 함께 사용하는 가장 강력한 워크플로우는 데스크톱에서 AI 코딩 에이전트를 시작하고 모바일에서 원활하게 이어받는 것입니다 — 또는 그 반대도 가능합니다. 두 클라이언트 모두 전체 스크롤백 기록을 포함하여 정확히 동일한 터미널 상태를 볼 수 있습니다.

### 데스크톱에서 세션 시작

이름이 지정된 tmux 세션을 만듭니다:

```bash
tmux new -s code
```

세션 내에서 AI 에이전트를 시작합니다:

```bash
claude
```

에이전트는 tmux 내에서 실행됩니다. **Ctrl+B**를 누른 다음 **D**를 눌러 언제든지 분리할 수 있습니다 — 세션과 그 안에서 실행되는 모든 것이 백그라운드에서 계속 실행됩니다.

### 모바일에서 연결하기

1. Spck Editor를 열고 CLI 서버에 연결합니다
2. Spck Editor 터미널 패널에서 터미널을 엽니다
3. 실행 중인 tmux 세션에 연결합니다:

```bash
tmux attach -t code
```

데스크톱과 정확히 동일한 터미널이 표시됩니다 — 실행 중인 에이전트, 출력, 전체 스크롤백 기록을 포함하여. 여러 클라이언트가 동시에 연결하여 실시간 출력을 볼 수 있습니다.

### 데스크톱으로 돌아가기

언제든지 임의의 터미널에서 다시 연결합니다:

```bash
tmux attach -t code
```

## <a name="use-case-2-persistent-cli-on-a-remote-server"></a>사용 사례 2: 원격 서버에서 지속적인 CLI 실행

SSH를 통해 원격 서버에서 Spck CLI를 실행하면 SSH 세션이 종료되는 순간 CLI도 중단됩니다 — 노트북을 닫거나, Wi-Fi를 잃거나, 연결이 타임아웃되는 경우에도 마찬가지입니다. Tmux는 연결 상태와 관계없이 서버에서 프로세스를 계속 실행합니다.

### 원격 서버 설정

서버에 SSH로 접속하고 CLI를 시작하기 전에 이름이 지정된 tmux 세션을 시작합니다:

```bash
ssh user@your-server.com
tmux new -s spck
spck
```

이제 CLI가 서버의 tmux 내에서 실행됩니다. SSH 연결을 닫거나 완전히 끊어도 CLI는 계속 실행됩니다.

### 연결 해제 후 재연결하기

```bash
ssh user@your-server.com
tmux attach -t spck
```

CLI는 중단된 위치에서 정확히 재개됩니다. 모바일 클라이언트는 릴레이 서버를 통해 정상적으로 재연결할 수 있습니다.

### 실행 중인 세션 목록 보기

```bash
tmux ls
```

## <a name="linux-service"></a>대안: Linux 서비스

수동 tmux 관리 없이 부팅 시 CLI를 자동으로 시작하는 완전 자동화된 설정을 위해 Spck CLI를 systemd 서비스로 실행하세요.

### 서비스 파일 만들기

```bash
sudo nano /etc/systemd/system/spck-cli.service
```

```ini
[Unit]
Description=Spck CLI Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/project
ExecStart=/usr/bin/npx spck
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

`your-username`과 `/path/to/your/project`를 실제 값으로 교체하세요. `spck`를 전역 설치했다면(`npm install -g spck`) `ExecStart`를 `which spck`의 출력으로 교체하세요.

### 활성화 및 시작

```bash
sudo systemctl daemon-reload
sudo systemctl enable spck-cli
sudo systemctl start spck-cli
```

### 상태 및 로그 확인

```bash
# 상태 보기
sudo systemctl status spck-cli

# 실시간 로그 추적
journalctl -u spck-cli -f
```

서비스는 매 재부팅 시 자동으로 시작되며 프로세스가 충돌하면 자동으로 재시작됩니다.

## <a name="essential-tmux-commands"></a>필수 Tmux 명령어

| 명령어 | 동작 |
| --- | --- |
| `tmux new -s name` | 이름이 지정된 새 세션 만들기 |
| `tmux attach -t name` | 기존 세션에 연결 |
| `tmux ls` | 모든 세션 나열 |
| `tmux kill-session -t name` | 세션 종료 |
| Ctrl+B, D | 세션에서 분리(계속 실행됨) |
| Ctrl+B, C | 새 창 만들기 |
| Ctrl+B, N | 다음 창으로 전환 |
| Ctrl+B, P | 이전 창으로 전환 |
| Ctrl+B, [ | 스크롤 모드 진입(화살표 키 / PgUp / PgDn) |
| Q | 스크롤 모드 종료 |
