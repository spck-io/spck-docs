# <a name="cli-configuration"></a>CLI 구성

## <a name="configuration"></a>구성

### 구성 파일 위치

구성은 프로젝트 디렉터리의 `.spck-editor/config/spck-cli.config.json`에 저장됩니다.

**중요**: `.spck-editor/config`는 `~/.spck-editor/projects/{project_id}/`를 가리키는 **심볼릭 링크**로, 시크릿을 프로젝트 디렉터리 외부에 보관합니다.

### 기본 구성

```json
{
  "version": 1,
  "root": "/path/to/your/project",
  "name": "My Project",
  "terminal": {
    "enabled": true,
    "maxBufferedLines": 10000,
    "maxTerminals": 10
  },
  "security": {
    "userAuthenticationEnabled": false
  },
  "filesystem": {
    "maxFileSize": "10MB",
    "watchIgnorePatterns": [
      "**/.git/**",
      "**/.spck-editor/**",
      "**/node_modules/**",
      "**/*.log",
      "**/.DS_Store",
      "**/dist/**",
      "**/build/**"
    ]
  },
  "browserProxy": {
    "enabled": true
  }
}
```

### 브라우저 프록시 설정

- **`browserProxy.enabled`** (boolean): 브라우저 프록시 기능 활성화/비활성화
  - 기본값: `true`
  - `false`로 설정하면 모바일 앱이 CLI를 통해 브라우저 프록시 세션을 열지 못하도록 합니다.

### 터미널 설정

- **`terminal.enabled`** (boolean): 터미널 접근 활성화/비활성화
  - 기본값: `true`
  - 터미널에 대한 무단 접근 위험을 줄이려면 `false`로 설정하세요.

- **`terminal.maxBufferedLines`** (number): 최대 스크롤백 버퍼
  - 기본값: `10000`
  - 메모리 사용량에 영향을 줍니다 (10,000줄당 약 1MB)

- **`terminal.maxTerminals`** (number): 최대 동시 터미널 세션 수
  - 기본값: `10`
  - 각 터미널은 약 5~10MB의 메모리를 사용합니다.

### 파일시스템 설정

- **`filesystem.maxFileSize`** (string): 읽기/쓰기 최대 파일 크기
  - 기본값: `"10MB"`
  - 허용 값: `"5MB"`, `"50MB"` 등

- **`filesystem.watchIgnorePatterns`** (string[]): 파일 감시에서 제외할 패턴
  - 기본값: 빌드 출력 및 의존성 무시
  - 수천 개의 생성된 파일을 피해 성능을 향상시킵니다.

### 보안 설정

- **`security.userAuthenticationEnabled`** (boolean): Firebase 사용자 인증 활성화
  - 기본값: `false`
  - `false`인 경우: 낮은 지연 시간, Lite와 호환, 시크릿 서명으로 여전히 보호됨
  - `true`인 경우: 추가 보안 레이어, 사용자 신원 확인, 첫 연결 시 2~20초의 초기 지연 추가
  - **이 설정에 관계없이 모든 요청은 항상 암호화 서명됩니다**

## <a name="security"></a>보안

### 암호화된 연결

모든 통신에 사용:

- **WSS (WebSocket Secure)**: TLS/SSL 암호화
- **HTTPS**: 암호화된 초기 핸드셰이크

### 요청 서명

모든 요청은 암호화 서명됩니다:

- 시크릿 키는 로컬에서 생성되며 인터넷을 통해 전송되지 않습니다.
- 시크릿 키가 노출될 수 있는 서드파티 QR 스캐너 사용은 권장하지 않습니다.

### 모범 사례

1. **자격 증명 보호**:

   ```bash
   # Add to .gitignore (automatic during setup)
   echo ".spck-editor/" >> .gitignore
   ```

2. **공유 기기에서 로그아웃**:

   ```bash
   spck --logout
   ```

3. **노출 디렉터리 제한**:

   ```bash
   # Instead of entire home directory
   spck --root /path/to/specific/project
   ```

4. **필요하지 않은 경우 터미널 비활성화**:

   ```json
   {
     "terminal": {
       "enabled": false
     }
   }
   ```

5. **필요하지 않은 경우 브라우저 프록시 비활성화**:
   ```json
   {
     "browserProxy": {
       "enabled": false
     }
   }
   ```

## <a name="user-authentication"></a>사용자 인증

Spck CLI는 항상 활성화된 요청 서명 위에 두 번째 보안 레이어로 선택적 Firebase 사용자 인증을 지원합니다.

### 작동 방식

활성화되면 CLI는 Spck Editor 계정으로 로그인해야 합니다. 연결은 매 시간마다 만료되는 Firebase ID 토큰을 사용하여 인증되며, `~/.spck-editor/.credentials.json`에 저장된 보안 갱신 토큰을 사용하여 자동으로 갱신됩니다.

### 사용자 인증 활성화

```json
{
  "security": {
    "userAuthenticationEnabled": true
  }
}
```

### 장단점

|  | 비활성화 (기본값) | 활성화 |
| -------------------- | ---------------------- | ----------------------------------- |
| **보호** | 시크릿 서명 키 | + Firebase 신원 확인 |
| **초기 지연** | 인증 오버헤드 없음 | 첫 연결 시 2~20초 추가 |
| **Spck Editor Lite** | ✅ 지원됨 | ❌ 미지원 |
| **오프라인 사용** | 인터넷 없이 작동 | 토큰 갱신을 위해 인터넷 필요 |

### 활성화 시점

**비활성화(기본값) 상태를 유지해야 하는 경우:**

- **Spck Editor Lite** 사용 시 — Firebase 로그인은 Lite에서 지원되지 않으며, `true`로 설정하면 Lite 사용자가 연결할 수 없게 됩니다.
- 로컬 네트워크 또는 시크릿 서명 키로 충분한 신뢰할 수 있는 환경에서 작업 시
- 연결 지연 시간을 최소화하는 것이 우선순위인 경우

**활성화해야 하는 경우:**

- CLI가 인터넷에서 접근 가능한 서버에 노출되어 있는 경우
- 서명 키 외에 추가적인 접근 제어 레이어로 사용자 신원 확인이 필요한 경우

> ⚠️ **Spck Editor Lite는 Firebase 인증을 지원하지 않습니다.** `userAuthenticationEnabled`가 `true`로 설정되면 Spck Editor Lite가 연결할 수 없습니다. Lite를 사용할 때는 이 설정을 `false`로 유지하세요.
