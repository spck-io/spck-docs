# <a name="claude-skill"></a>Claude 스킬: Spck CLI를 Linux 서비스로 실행하기

이 페이지는 Linux에서 Spck CLI(`spck`)를 `systemd` 서비스로 설치하는 것을 자동화하는 다운로드 가능한 [Claude Code 스킬](https://docs.claude.com/en/docs/claude-code/skills)을 제공합니다. 스킬이 설치되면 Claude Code에 "spck를 서비스로 실행해 줘"라고 요청하면 환경을 확인하고, 실제 절대 경로가 포함된 올바른 유닛 파일을 생성하여 설치하고, 정상적으로 실행되는지 확인합니다 — 체크리스트에서 명령을 복사해 붙여넣을 필요가 없습니다.

이 스킬은 [Tmux 사용하기 → 대안: Linux 서비스](./tmux#linux-service)에 설명된 것과 동일한 systemd 설정을, 유닛 파일을 수동으로 작성할 때 놓치기 쉬운 사전 점검 및 실패 진단과 함께 자동화합니다.

## <a name="download"></a>다운로드

스킬 파일을 다운로드하여 로컬 Claude Code 스킬 디렉토리에 저장합니다:

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

또는 수동으로 다운로드: <a href="/assets/skills/spck-cli-service/SKILL.md" download>SKILL.md</a> — `~/.claude/skills/spck-cli-service/SKILL.md`에 배치하세요.

## <a name="what-the-skill-does"></a>스킬이 하는 일

호출되면 스킬은 Claude Code를 전체 설치 과정으로 안내합니다:

1. 호스트가 `systemd`를 실행하는 Linux인지 확인합니다.
2. `spck`의 절대 경로를 확인합니다(`ExecStart`를 망가뜨리는 `PATH` 불일치 방지).
3. `node`가 `nvm`을 통해 설치된 경우 경고합니다 — 해당 경로는 Node 업그레이드마다 변경되어 유닛을 조용히 망가뜨립니다.
4. `~/.spck-editor/.credentials.json`이 존재하는지 확인합니다(CLI는 서비스로 실행하기 전에 최소 한 번은 대화형으로 실행되어야 합니다).
5. 필요에 따라 **사용자 서비스**(`systemctl --user`, `sudo` 불필요)와 **시스템 서비스** 중에서 선택합니다.
6. 실제 경로가 입력된 유닛 파일을 작성합니다 — 플레이스홀더 없음.
7. `daemon-reload`, `enable --now`를 실행한 다음 저널을 추적하여 CLI가 릴레이 서버에 연결되었는지 확인합니다.

스킬은 또한 가장 흔한 7가지 실패 모드(잘못된 `ExecStart` 경로, 자격 증명 없음, 프로젝트 디렉토리 권한 오류, `start-limit-hit`에 도달한 재시작 루프, npm 업그레이드 후 오래된 nvm 경로 등)를 문서화하여 Claude Code가 유닛 파일을 재생성하는 대신 망가진 서비스를 진단할 수 있도록 합니다.

## <a name="installation"></a>설치

<div class="ptabs">
  <div class="ptabs-nav">
    <button type="button" class="ptabs-btn" data-tab="claude-code">Claude Code (CLI)</button>
    <button type="button" class="ptabs-btn" data-tab="claude-desktop">Claude Desktop</button>
  </div>
  <div class="ptabs-body">
    <div class="ptabs-pane" data-tab="claude-code">

**1단계 — 스킬 파일 다운로드:**

```bash
mkdir -p ~/.claude/skills/spck-cli-service
curl -fsSL https://docs.spck.io/assets/skills/spck-cli-service/SKILL.md \
  -o ~/.claude/skills/spck-cli-service/SKILL.md
```

**2단계 — Claude Code가 인식했는지 확인:**

```bash
claude /skills
```

목록에 `spck-cli-service`가 보여야 합니다. 보이지 않으면 Claude Code를 재시작하여 스킬 디렉토리를 다시 스캔하도록 하세요.

</div>
    <div class="ptabs-pane" data-tab="claude-desktop">

Claude Desktop은 macOS와 Linux에서 동일한 `~/.claude/skills/` 디렉토리에서 스킬을 로드합니다. Windows에서 경로는 `%USERPROFILE%\.claude\skills\`이지만, 스킬 자체는 Linux 호스트에서만 작동하므로 Claude Desktop을 실행하는 컴퓨터가 아닌 `spck`를 실행하려는 컴퓨터에 설치하세요.

원격 Linux 서버를 관리하는 경우, 해당 서버에서 SSH를 통해 Claude Code를 실행하세요(또는 서버에 대한 완전한 셸을 제공하는 Spck CLI 터미널을 통해). 로컬 Mac에 스킬을 설치하면 원격 Linux 서비스를 구성하는 데 도움이 되지 않습니다.

</div>
  </div>
</div>

## <a name="usage"></a>사용법

설치 후, Claude Code에 자연어로 요청하여 스킬을 호출합니다. 스킬을 트리거하는 예시:

- "spck를 systemd 서비스로 설치해 줘"
- "Spck CLI가 부팅 시 시작하도록 만들어 줘"
- "내 spck-cli.service가 계속 재시작되는데, 디버그해 줄 수 있어?"
- "SSH가 끊어져도 살아남도록 spck를 데몬으로 실행해 줘"

Claude Code는 스킬을 읽고, 사전 점검을 실행하며(각 명령을 승인하라는 프롬프트가 표시됩니다), 유닛 파일을 생성하여 설치합니다. 승인 전에 각 명령을 검토하세요 — 특히 `sudo`로 `/etc/systemd/system/`에 쓰는 명령은 주의가 필요합니다.

## <a name="what-gets-installed"></a>설치되는 항목

스킬은 단일 유닛 파일을 설치합니다. 사용자 서비스의 경우:

```bash
~/.config/systemd/user/spck-cli.service
```

내용은 다음과 같습니다:

```ini
[Unit]
Description=Spck CLI Server
After=network-online.target
Wants=network-online.target

[Service]
Type=simple
WorkingDirectory=%h/your-project
ExecStart=/usr/local/bin/spck
Restart=on-failure
RestartSec=5
StartLimitIntervalSec=60
StartLimitBurst=5

[Install]
WantedBy=default.target
```

시스템 서비스의 경우, 파일은 `/etc/systemd/system/spck-cli.service`에 위치하며 `User=`와 `Group=` 지시어가 추가됩니다. 스킬은 환경에 따라 적절한 변형을 선택하고 실제 절대 경로를 파일에 기록합니다.

## <a name="why-a-skill-instead-of-copy-paste"></a>복사-붙여넣기 대신 스킬을 사용하는 이유

[tmux 문서](./tmux#linux-service)의 유닛 파일은 출발점이지만, 서비스가 실제로 작동하려면 여러 가지가 올바르게 설정되어야 합니다:

- `ExecStart`는 `spck`의 **절대 경로**여야 합니다. 로그인 셸 내에서 `which spck`는 systemd가 보지 못하는 `.bashrc`의 PATH 조작을 해결합니다.
- `spck`가 `nvm` 아래에 설치된 경우, 경로에 Node 버전이 포함됩니다 — Node를 업그레이드하면 다음 재부팅까지 서비스가 조용히 망가집니다.
- `~/.spck-editor/.credentials.json`을 생성하려면 CLI가 최소 한 번은 대화형으로 실행되어야 합니다. 자격 증명 없이 새로 서비스를 시작하면 명백한 오류 없이 깔끔하게 종료됩니다.
- `User=`는 `WorkingDirectory`를 소유해야 합니다. 그렇지 않으면 파일 감시가 `EACCES`에 부딪히고 CLI가 재시작 루프에 들어갑니다.
- 사용자 서비스는 헤드리스 서버에서 `loginctl enable-linger`가 필요합니다. 그렇지 않으면 로그인 세션이 활성화된 동안에만 실행됩니다.

스킬은 이 모든 것을 자동화하므로 기억할 필요가 없습니다.

## <a name="uninstall"></a>제거

서비스를 비활성화하고 제거합니다:

```bash
systemctl --user disable --now spck-cli
rm ~/.config/systemd/user/spck-cli.service
systemctl --user daemon-reload
```

시스템 서비스의 경우:

```bash
sudo systemctl disable --now spck-cli
sudo rm /etc/systemd/system/spck-cli.service
sudo systemctl daemon-reload
```

Claude Code에서 스킬 자체를 제거하려면:

```bash
rm -rf ~/.claude/skills/spck-cli-service
```

## <a name="see-also"></a>참고 항목

- [Tmux 사용하기](./tmux) — SSH 연결이 끊어져도 CLI를 유지하기 위한 `tmux`를 사용하는 대안적 접근법.
- [고급 사용법](./cli-advanced) — 전체 CLI 명령 참조, 구성 재정의, 다중 프로젝트 설정.
- [구성](./cli-config) — 유닛 파일이 다루지 않는 터미널, 파일 시스템, 보안 및 인증 설정.
