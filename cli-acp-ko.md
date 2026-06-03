# <a name="ai-coding-agents-acp"></a>모바일에서의 AI 코딩 에이전트 (ACP)

Spck Editor의 **AI Chat**을 통해 **Claude Code**, **OpenAI Codex**, 또는 **Gemini CLI**를 휴대폰에서 직접 실행하세요. Spck CLI는 개방형 [Agent Client Protocol (ACP)](https://agentclientprotocol.com/)를 통해 에디터를 로컬에 설치된 에이전트 CLI와 연결하여, 모델이 모바일 기기에서 감독하는 동안 사용자의 머신에서, 사용자의 구독으로, 실제 파일에 대해 실행되도록 합니다.

![Spck Editor의 AI Chat에서 ACP 로컬 AI 모드로 휴대폰에서 데스크톱의 Claude Code를 구동하는 모습](https://docs.spck.io/assets/gifs/acp-ai.gif)

## <a name="acp-overview"></a>ACP란 무엇이며 왜 사용하는가?

Agent Client Protocol (ACP)은 Language Server Protocol (LSP)과 같은 정신에 따라 에디터 ↔ AI 에이전트 통신을 위한 Zed Industries의 개방형 표준입니다. Spck CLI 0.6.0+는 ACP를 구현하며, Spck Editor의 AI Chat (클라이언트)과 설치된 모든 ACP 호환 에이전트 바이너리 (에이전트) 사이의 **트랜스포트** 역할을 합니다.

인앱 서버 라우팅 AI Chat과 비교했을 때, 로컬 ACP 경로는 다음을 제공합니다:

- **본인의 구독** — 에이전트 호출은 Spck Editor AI 할당량이 아닌 Claude Code / ChatGPT / Gemini 계정에 청구됩니다.
- **실제 파일시스템 접근** — 에이전트는 에디터의 메모리 내 복사본이 아니라 CLI를 통해 디스크의 실제 파일을 읽고 씁니다.
- **네이티브 도구** — 파일 워처, 언어 서버, 셸 명령이 실제 머신에서 실행됩니다.
- **데스크톱과의 연속성** — 책상에서 사용하는 동일한 `claude` / `gemini` / `codex` 로그인이 모바일 채팅을 구동합니다.

## <a name="acp-supported-agents"></a>지원되는 AI 에이전트

원하는 에이전트를 설치하세요. Spck CLI가 시작 시 자동으로 감지합니다.

| 에이전트          | 설치                                                                                 |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Claude Code**   | [`claude`](https://docs.claude.com/en/docs/claude-code/setup)                        |
| **OpenAI Codex**  | `npm install -g @agentclientprotocol/codex-acp`                                      |
| **Gemini CLI**    | [`gemini`](https://github.com/google-gemini/gemini-cli)                              |

## <a name="acp-installation"></a>설치 및 설정

### 1. Spck CLI 설치

아직 없다면:

```bash
npm install -g spck
# 또는 설치 없이 실행
npx spck
```

전체 첫 실행 마법사는 [Spck CLI 시작하기](./cli-start)를 참조하세요.

### 2. 하나 이상의 에이전트 CLI 설치

사용 가능하게 하고 싶은 에이전트를 선택하세요. 여러 개를 설치할 수 있으며 — AI Chat은 세션별로 그 중에서 선택할 수 있게 합니다. 설치 명령은 위의 [지원되는 AI 에이전트](#acp-supported-agents) 표를 참조하세요.

### 3. 각 에이전트를 한 번 인증

에이전트 CLI는 각각 Spck Editor 외부에서 자체 로그인을 관리합니다:

```bash
claude            # Anthropic Claude Code 로그인 플로우
codex login       # OpenAI Codex 로그인 플로우 (codex-acp가 사용)
gemini            # Google Gemini 로그인 플로우
```

이 단계를 건너뛰면 채팅을 처음 시작할 때 Spck Editor가 `ACP agent requires authentication; run <binary> login and retry`와 같은 오류를 표시합니다.

### 4. Spck CLI 시작

```bash
cd /path/to/your/project
spck
```

시작 시 CLI는 어떤 에이전트가 사용 가능한지 나열하는 에이전트별 감지 보고서를 출력하며, 이어서 주 기능 블록에 `✅ ACP agents: Claude Code, Gemini CLI`와 같은 한 줄 요약이 표시됩니다. 아무것도 사용할 수 없으면 대신 서버 라우팅 AI Chat으로 대체됩니다.

### 5. Spck Editor 연결

QR 코드를 스캔하거나 [수동 입력](./cli-start#connecting)을 사용하세요. 연결되면 Spck Editor에서 **AI Chat**을 열면 — 트랜스포트 스위처가 클라우드 옵션과 함께 로컬 에이전트를 표시합니다.

## <a name="acp-authentication"></a>인증

각 에이전트는 Spck CLI가 실행되는 머신에서 자체 자격 증명을 관리합니다. 에이전트당 한 번씩 로그인 플로우를 실행하세요:

```bash
# Claude Code
claude

# Codex (codex-acp는 Codex CLI 자체 로그인을 래핑)
codex login

# Gemini CLI
gemini
```

재설치하거나 머신을 옮긴 경우 새 호스트에서 로그인을 반복하세요. 인증은 **호스트별, 에이전트별** 입니다 — Spck Editor 자체는 이러한 자격 증명을 보유하지 않습니다.

## <a name="acp-billing"></a>요금 청구 및 사용량 제한

ACP는 본인의 자격 증명으로 본인의 머신에서 에이전트를 실행하므로, **모든 사용량은 해당 제공자의 본인 계정에 청구됩니다** — Spck Editor 구독에 청구되지 않습니다. 이 모드에서 Spck Editor와 Spck 릴레이 서버는 순수 트랜스포트로 동작하며 ACP 트래픽에 대해 앱 내 AI 할당량을 소비하지 않습니다.

### Claude Code 요금 청구

> ⚠️ **중요 — Claude Code는 타사 도구에 의해 구동될 때 별도의 사용량 제한 버킷을 적용합니다.**
>
> Claude Code가 ACP를 통해 타사 클라이언트에서 호출되면 Anthropic은 해당 트래픽을 Pro / Max 구독의 대화형 `claude` CLI 세션과 **다른 사용량 제한 버킷**에 계산합니다. 실질적인 결과: 대화형 Claude Code 여유가 남아있는데도 타사 버킷을 소진할 수 있으며 (또는 그 반대), 두 버킷을 합칠 수 없습니다.
>
> 현재 소비량은 `claude` 안에서 `/usage`와 [Anthropic Console](https://platform.claude.com/usage)을 확인하고, 사용 중인 플랜에 적용되는 수치는 [Claude Code 비용 및 제한 문서](https://code.claude.com/docs/en/costs)를 검토하세요.

### Codex (codex-acp) 요금 청구

OpenAI Codex CLI 자체 인증을 통해 청구됩니다 — 본인의 OpenAI API 키 또는 ChatGPT 로그인입니다. 사용량은 해당 계정이 가진 어떤 플랜에 대해 계산됩니다. 가격과 할당량은 대화형 `codex` 사용과 동일합니다; 현재 수치는 [openai.com/codex](https://github.com/openai/codex)와 OpenAI 대시보드를 참조하세요.

### Gemini CLI 요금 청구

본인의 Google 계정이나 Gemini API 키를 통해 청구됩니다. 사용량은 해당 로그인에 연결된 Gemini 플랜 또는 API 할당량에 대해 계산됩니다. 사용량 제한 상세는 [ai.google.dev](https://ai.google.dev/gemini-api/docs/rate-limits)를 참조하세요.

## <a name="acp-configuration"></a>구성

ACP는 기본적으로 활성화되어 있으며 프로젝트의 `spck-cli.config.json`을 통해 구성됩니다:

```json
{
  "acp": {
    "enabled": true
  }
}
```

전체 스키마는 [구성 → ACP 설정](./cli-config#acp-settings)을 참조하세요.

### 프로젝트별 ACP 비활성화

이 호스트에서 Spck Editor가 로컬 에이전트를 구동할 수 없게 하려면:

```json
{
  "acp": {
    "enabled": false
  }
}
```

비활성화되면 에디터의 트랜스포트 스위처는 로컬 에이전트 옵션을 숨기고 모든 `acp.*` RPC는 `FEATURE_DISABLED`로 거부됩니다. 설정 마법사는 첫 실행 시 이 질문을 합니다 (기본값 `Y`); 이 옵션 이전의 구성은 `acp.enabled: true`가 자동으로 추가되어 로드되고 다시 저장됩니다.

### 단일 에이전트 비활성화

다른 에이전트에 대해 ACP를 활성화한 상태에서 _특정_ 에이전트가 제공되지 않도록 하려면 해당 에이전트의 바이너리를 제거하세요. 감지는 CLI가 시작될 때마다 실행되므로 에디터의 트랜스포트 스위처가 목록에서 제거합니다.

## <a name="acp-vs-server-routed"></a>로컬 ACP 대 서버 라우팅 AI Chat

| 기능                                       | 서버 라우팅 (기본값, CLI 없음)     | 로컬 (ACP, CLI 연결됨)                  |
| ------------------------------------------ | ---------------------------------- | --------------------------------------- |
| 모델 실행 위치                              | Spck 클라우드                      | 본인 머신                               |
| 자격 증명                                  | 본인의 Spck Editor 계정            | 에이전트 자체 로그인 / API 키           |
| 파일 접근                                  | 에디터의 메모리 내 파일시스템     | CLI 루트를 통한 디스크의 실제 파일      |
| Spck Editor AI 할당량 차감                 | 예                                 | **아니오** — 에이전트 제공자에 청구     |
| CLI 실행 없이 작동                         | 예                                 | 아니오 (CLI + WebSocket 필요)           |
| 사용 가능한 에이전트                       | Spck 호스팅 모델                   | Claude Code, Codex, Gemini CLI          |
| 휴대폰의 도구 사용 권한 프롬프트           | 해당하는 경우                      | 예, ACP를 통해 전달됨                   |
| 토큰 스트리밍                              | 예                                 | 예                                      |
| 멀티턴 채팅                                | 예                                 | 예                                      |

프로젝트 중간에 트랜스포트를 전환할 수 있습니다 — AI Chat은 CLI 연결 상태와 감지된 에이전트를 기반으로 현재 사용 가능한 경로를 표시합니다.

## <a name="acp-tmux"></a>장시간 세션을 위한 Tmux와의 결합

ACP 세션은 에디터 재연결을 견디지만, Spck CLI 프로세스 자체는 터미널이 닫히면 종료됩니다. 대규모 리팩터링, 수 시간의 계획 세션 등 장시간 에이전트 작업의 경우, SSH 연결 끊김, 터미널 종료, 노트북 슬립을 견딜 수 있도록 [tmux](./tmux) 세션 내에서 CLI를 시작하세요:

```bash
tmux new -s spck
spck
# Ctrl+B 다음 D로 detach
```

휴대폰에서 Spck CLI 터미널을 통해 다시 연결하고 `tmux attach -t spck`로 에이전트를 라이브로 모니터링할 수도 있습니다. 영구 백그라운드 서비스로 CLI를 실행하는 것을 포함한 전체 패턴은 [Tmux 사용하기](./tmux#use-case-1-sharing-agent-sessions-across-desktop-and-mobile)를 참조하세요.

Linux 호스트의 경우, [Claude Skill: Linux Service](./claude-skill) 페이지는 Spck CLI를 `systemd` 서비스로 실행하기 위한 단일 명령 설정을 제공하므로 WebSocket과 그 위의 모든 ACP 세션이 부팅 시 자동으로 시작됩니다.

## <a name="acp-faq"></a>자주 묻는 질문

### 휴대폰에서 Claude Code를 사용할 수 있나요?

예. 데스크톱에 Claude Code를 설치하고 `claude`로 인증한 다음 프로젝트에서 `spck`를 실행하세요. 휴대폰에서 Spck Editor를 연결하고 AI Chat의 트랜스포트 스위처에서 Claude Code를 선택하세요. 모델은 본인의 구독으로 데스크톱에서 실행되며, 휴대폰에서 구동합니다.

### Spck Editor가 내 Claude / OpenAI / Gemini API 키를 보나요?

아니오. 각 에이전트 CLI는 Spck CLI가 실행되는 머신에서 자체 자격 증명을 관리합니다. ACP 메시지는 휴대폰과 CLI 사이의 암호화된 WebSocket을 통해 터널링되지만 에이전트 자체 인증 토큰은 호스트를 벗어나지 않습니다.

### Spck Editor를 통해 Claude Code를 사용하는 데 추가 비용이 있나요?

추가 Spck Editor 요금은 없습니다. 에이전트의 사용량은 책상에서 대화형으로 에이전트를 실행하는 것과 정확히 같은 방식으로 본인의 Anthropic / OpenAI / Google 플랜에 계산됩니다 — 단, Anthropic은 타사 클라이언트에 대해 별도의 사용량 제한 버킷을 적용합니다; 위의 [요금 청구 및 사용량 제한](#acp-billing)을 참조하세요.

### ACP를 사용하려면 유료 Spck Editor 구독이 필요한가요?

아니오. 무료 등급 (하루 30분 CLI 연결)은 어떤 ACP 에이전트든 구동하기에 충분합니다. 앱 내 서버 라우팅 AI Chat만 Spck Editor AI 할당량을 소비합니다.

### 채팅 중에 Wi-Fi 연결이 끊기면 어떻게 되나요?

에이전트 프로세스는 CLI 호스트에서 계속 살아 있습니다. 에디터가 다시 연결되면 전체 채팅 기록과 함께 세션이 재개됩니다. 오프라인 동안 도착한 스트리밍 출력은 재연결 시 재생됩니다.

### 노트북 대신 원격 서버에서 에이전트를 실행할 수 있나요?

예. 도달 가능한 모든 Linux/macOS 호스트 — 개발 VM, 홈 서버, 워크스테이션 — 에서 Spck CLI를 실행하고 릴레이 서버를 통해 연결할 수 있습니다. 연결 간 CLI를 계속 살아있게 하려면 [tmux](./tmux) 또는 [systemd 스킬](./claude-skill)과 결합하세요.

### ACP가 Spck Editor Lite와 함께 작동하나요?

예. ACP 트래픽은 Spck Editor Lite가 지원하는 파일시스템 및 git과 동일한 WebSocket 트랜스포트를 사용합니다. CLI 구성에서 `security.userAuthenticationEnabled`가 `false`로 설정되어 있는지 확인하세요 — Firebase 인증은 Lite에서 지원되지 않습니다. [구성 → 사용자 인증](./cli-config#user-authentication)을 참조하세요.

### AI Chat에 내 에이전트가 표시되지 않는 이유는 무엇인가요?

CLI 시작 로그에서 에이전트별 라인을 확인하세요:

- 에이전트가 감지되지 않음 — 설치하세요 ([지원되는 AI 에이전트](#acp-supported-agents) 참조).
- 감지되었지만 에디터에 없음 — 에이전트 자체 로그인 플로우를 완료했는지 확인하세요 (`claude`, `codex login`, `gemini`).
- ACP 비활성화됨 — `.spck-editor/config/spck-cli.config.json`에서 `acp.enabled`를 확인하세요. [구성](./cli-config#acp-settings) 참조.

## <a name="acp-troubleshooting"></a>문제 해결

### 에이전트는 감지되었지만 세션이 시작되지 않음

대개 에이전트가 인증되지 않았음을 의미합니다. CLI 호스트에서 에이전트의 로그인 플로우를 실행하세요:

```bash
claude              # 그 다음 브라우저 인증 완료
codex login
gemini
```

문제가 지속되면 `.spck-editor/logs/`의 CLI 로그에서 에이전트의 stderr 출력을 확인하세요. 일반적으로 실패한 인증이나 바이너리를 가리킵니다.

### 채팅 중 사용량 제한 오류

Claude Code의 경우 에디터는 Anthropic의 429를 그대로 표시합니다. [Anthropic Console 사용량 페이지](https://platform.claude.com/usage)와 [Claude Code 비용 문서](https://code.claude.com/docs/en/costs)를 확인하세요 — 타사 사용량 제한 버킷이 대화형 `claude` 할당량과 별개임을 기억하세요.

Codex와 Gemini의 경우 에디터는 제공자 자체의 할당량 오류를 표시합니다. 제공자 콘솔을 통해 해결하세요.

### ACP 세션 시작 시 CLI 충돌

Spck CLI는 ACP 트래픽을 `.spck-editor/logs/`에 기록합니다. 문제를 재현하는 동안 최신 로그 파일을 추적하세요:

```bash
tail -f .spck-editor/logs/spck-*.log
```

관련 스니펫과 함께 [github.com/spck-editor](https://github.com/spck-editor)에 버그를 보고하세요.

### 에이전트가 프로젝트 루트 외부에서 변경하는 경우

ACP 에이전트는 CLI의 구성된 `root` 디렉터리로 범위가 한정됩니다. 그 외부에 쓰기가 나타나면 이슈를 제출하세요 — 이런 일은 발생해서는 안 됩니다. 임시 방편으로 `spck --root /path/to/specific/project`를 실행해 범위를 더 좁히세요.

## <a name="acp-see-also"></a>관련 항목

- [Spck CLI 시작하기](./cli-start) — 처음 설치, 인증, 연결
- [CLI 참조](./cli) — 릴레이 서버, 일일 워크플로, 연결 제한
- [구성 → ACP 설정](./cli-config#acp-settings) — `acp.enabled` 구성 옵션
- [고급 사용법](./cli-advanced) — CLI 플래그, 여러 프로젝트, 모바일 프롬프트 팁
- [Tmux 사용하기](./tmux) — 재연결을 거치며 ACP 세션 유지
- [Claude Skill: Linux Service](./claude-skill) — Spck CLI를 `systemd` 서비스로 실행해 ACP가 항상 사용 가능하도록
- [Agent Client Protocol 사양](https://agentclientprotocol.com/) — ACP가 구현하는 개방형 표준
- [Claude Code 문서](https://docs.claude.com/en/docs/claude-code/overview)
- [Gemini CLI 저장소](https://github.com/google-gemini/gemini-cli)
- [OpenAI Codex CLI](https://github.com/openai/codex)
