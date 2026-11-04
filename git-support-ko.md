# <a name="git-support"></a>Git 지원

Spck는 Android와 iOS의 로컬 프로젝트, 브라우저, Spck CLI를 통한 원격 프로젝트에서 Git을 지원합니다. 이 가이드는 공급자 자격 증명, 풀 리퀘스트, 커밋 검사, 충돌 해결, 플랫폼 제한 사항을 다룹니다.

기본 Git 통합, 커밋 기록, 병합 충돌 해결은 무료 버전에서 사용할 수 있습니다. [향상된 Git 통합](#enhanced-git-integration)은 풀 리퀘스트 관리와 커밋 파일 diff를 추가합니다.

## <a name="git-credentials"></a>Git 자격 증명 및 풀 리퀘스트

**Git menu → Git Credentials**를 열고 공급자를 선택한 다음 액세스 토큰을 저장하세요. 아래 설정 및 도움말 링크는 새 탭에서 열리므로 Spck로 돌아와 토큰을 붙여넣을 수 있습니다.

| 공급자 | 토큰 설정 | Git 및 풀 리퀘스트 권한 |
| --- | --- | --- |
| GitHub | <a href="https://github.com/settings/personal-access-tokens/new?contents=write&amp;pull_requests=write&amp;metadata=read&amp;name=Spck-Editor&amp;expires_in=90" target="_blank" rel="noopener noreferrer">GitHub 토큰 만들기</a> · <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens" target="_blank" rel="noopener noreferrer">설정 가이드</a> | 저장소를 선택하세요. 생성 링크는 **Contents: Read and write**, **Pull requests: Read and write**, **Metadata: Read**를 미리 선택합니다. |
| GitLab | <a href="https://gitlab.com/-/user_settings/personal_access_tokens?name=Spck-Editor&amp;scopes=api" target="_blank" rel="noopener noreferrer">GitLab 토큰 만들기</a> · <a href="https://docs.gitlab.com/user/profile/personal_access_tokens/#prefill-personal-access-token-details" target="_blank" rel="noopener noreferrer">설정 가이드</a> | 생성 링크는 머지 리퀘스트용 `api` 범위를 미리 선택합니다. |
| Bitbucket Cloud | <a href="https://id.atlassian.com/manage-profile/security/api-tokens" target="_blank" rel="noopener noreferrer">API 토큰 만들기</a> · <a href="https://support.atlassian.com/bitbucket-cloud/docs/create-an-api-token/" target="_blank" rel="noopener noreferrer">설정 가이드</a> | **Create API token with scopes**, **Bitbucket**을 선택하고 `read:repository:bitbucket`, `write:repository:bitbucket`, `read:pullrequest:bitbucket`, `write:pullrequest:bitbucket`을 수동으로 지정하세요. API 인증에는 Atlassian 계정 이메일을 사용합니다. |
| Azure DevOps | <a href="https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate" target="_blank" rel="noopener noreferrer">PAT 생성 가이드</a> | 조직의 **User settings → Personal access tokens → New Token**을 열고 조직을 선택한 뒤 **Code (Read & write)**를 수동으로 지정하세요. |

풀 리퀘스트를 만들려면 소스 브랜치를 커밋하고 푸시한 뒤 **Git menu → Create PR**를 여세요. 원격 저장소와 자격 증명, 다른 대상 브랜치를 선택하고 제목과 설명을 입력합니다. **Generate with AI**는 두 브랜치의 공통 조상 이후 커밋된 변경으로 메시지 초안을 작성할 수 있습니다. 먼저 대상 브랜치를 가져오세요. 초안을 검토한 뒤 **Create PR**를 선택합니다. GitLab에서는 머지 리퀘스트가 생성됩니다.

풀 리퀘스트 생성과 관리는 [향상된 Git 통합](#enhanced-git-integration)에 포함된 **Premium 기능**입니다. Lite는 일회성 앱 구매에 이 기능을 포함합니다. 전체 앱에서는 활성 Supporter, Gold 또는 Node 구독이 있는 계정이나 Spck for NodeJS 터미널 평생 이용권을 소유한 계정으로 로그인하세요.

## <a name="pull-request-management"></a>풀 리퀘스트 관리(Premium)

편집기를 떠나지 않고 풀 리퀘스트를 관리할 수 있습니다. 지원하는 원격 서비스는 **GitHub.com, GitLab.com, Bitbucket Cloud, Azure DevOps**입니다. GitLab에서는 머지 리퀘스트라고 합니다.

1. Git 프로젝트를 열고 위 권한을 가진 공급자 토큰을 **Git menu → Git Credentials**에 추가하세요.
2. **Branches menu → Pull Requests**를 열고 원격 저장소와 자격 증명을 선택하여 열린 요청을 표시하세요.
3. 요청을 선택하면 제목, 설명, 작성자, 소스·대상 브랜치와 상태를 볼 수 있습니다.
4. 변경된 파일을 선택하여 읽기 전용 diff를 검토한 뒤 병합을 결정하세요.
5. 병합 가능한 요청은 **Merge**, 병합 없이 닫으려면 **Close**를 사용하세요. 필수 검토, 검사, 토큰 권한 및 브랜치 규칙은 계속 적용됩니다. 초안과 충돌이 있는 요청은 이 대화 상자에서 병합할 수 없습니다.

공급자에서 변경한 후 **Refresh**로 목록을 갱신하세요. 요청 상세 정보에는 검토, 검사 및 다른 작업을 위한 공급자 링크도 있습니다.

새 요청은 위의 **Git menu → Create PR**로 시작합니다. 소스 브랜치를 푸시해야 하면 생성 전에 **Push**를 제공합니다. 선택적인 AI 초안 작성은 설정한 AI 서비스와 사용 한도를 이용하며 Lite에 포함된 풀 리퀘스트 이용 권한과는 별개입니다.

토큰 권한 때문에 생성에 실패하면 공급자 링크에서 토큰을 생성하거나 갱신하고 **Git Credentials**에 저장한 다음 다시 시도하세요. PR 초안은 유지됩니다.

## <a name="enhanced-git-integration"></a>향상된 Git 통합

향상된 Git 통합은 변경을 검토하고 공유하는 두 가지 도구를 추가합니다.

- **풀 리퀘스트 관리:** 요청 생성, 열린 요청 탐색, 변경 파일과 diff 검토, 병합 또는 닫기를 지원합니다. 설정과 절차는 [풀 리퀘스트 관리](#pull-request-management)를 참고하세요.
- **커밋 검사:** 작업 파일을 바꾸지 않고 커밋의 변경 파일과 diff를 검토합니다.

Git 패널의 **History** 탭에서 커밋을 선택하여 추가·수정·삭제된 파일을 확인하세요. 파일을 선택하면 커밋의 첫 번째 부모와 비교한 읽기 전용 diff가 열립니다. 첫 커밋은 빈 트리와 비교합니다. 뷰어는 커밋된 버전을 사용하므로 커밋하지 않은 편집은 diff에 영향을 주지 않습니다. 바이너리 파일은 텍스트 diff로 표시할 수 없습니다.

기록 항목을 길게 누르거나 마우스 오른쪽 버튼으로 클릭한 뒤 **View Commit**을 선택할 수도 있습니다.

향상된 Git 통합은 다음에 포함됩니다.

- **Spck Editor Lite:** 일회성 앱 구매로 영구 이용 가능하며 로그인은 필요 없습니다.
- **Spck for NodeJS 터미널 평생 구매:** 구매한 계정에서 영구 이용 가능하며 로그인이 필요합니다.
- **Supporter, Gold 또는 Node 구독:** 구독이 활성 상태인 동안 이용 가능하며 로그인이 필요합니다.

기본 Git 통합과 커밋 기록 탐색은 무료 버전에서도 계속 제공됩니다. 요금제 정보는 [가격](https://spck.io/pricing)을 참고하세요.

## <a name="merge-conflict-resolution"></a>병합 충돌 해결

diff 뷰어는 작업 파일의 충돌 해결도 지원합니다. 기본 Git 통합의 일부이며 Premium이 필요하지 않습니다.

1. Git 변경 목록에서 충돌한 파일을 여세요.
2. 각 충돌에 **Accept Current**, **Accept Incoming**, **Accept Both** 중 하나를 선택하세요. 파일을 직접 편집하여 변경을 수동으로 합칠 수도 있습니다.
3. 결과를 검토하세요. 충돌 마커를 모두 제거하면 diff 뷰어에서 **Resolve**를 선택해 해결한 파일을 스테이징하세요.
4. 나머지 파일도 해결한 뒤 병합을 커밋하세요.

터치 기기에서는 파일이나 Git 항목을 길게 눌러 컨텍스트 메뉴를 여세요. Git 상태 문자는 파일 이름 색상을 보완하여 변경을 쉽게 구분하게 합니다.

## <a name="git-limitations"></a>Git 제한 사항

### <a name="git-limitations-overview"></a>개요

Git 구현은 프로젝트 저장 위치와 Spck 버전에 따라 다릅니다.

| 환경 | Git 구현 | 주요 제약 |
| --- | --- | --- |
| Lite 및 Spck for NodeJS를 포함한 Android·iOS 앱 | 로컬 프로젝트용 네이티브 컴파일 **libgit2** | 기기 저장소의 프로젝트가 필요하며 기기 리소스와 파일 시스템 제한이 계속 적용됩니다. |
| 브라우저 및 임베디드 편집기 | JavaScript 기반 [isomorphic-git](https://isomorphic-git.org/) | 브라우저 메모리, 저장소 및 네트워크 제한이 적용됩니다. |
| Spck CLI를 통한 원격 프로젝트 | 호스트 컴퓨터의 **Git 바이너리** | 호스트의 리소스, 파일 시스템, 자격 증명 및 설치된 Git을 사용합니다. |

현재 모바일 빌드는 브라우저 Git 엔진 대신 네이티브 Git을 사용합니다. 로컬 작업에 **Native Git requires a device folder**가 표시되면 프로젝트를 기기 저장소로 옮기세요. 편집기의 브라우저 데이터베이스에만 저장된 프로젝트는 모바일 네이티브 Git 클라이언트를 사용할 수 없습니다.

풀 리퀘스트 관리는 **Git Credentials**에 저장한 토큰으로 공급자 API를 직접 호출합니다. 브라우저 로그인 쿠키를 사용하지 않고 API 응답을 캐시하지 않으므로 새로 고침 시 최신 요청 상태와 브랜치 정보를 가져올 수 있습니다. 권한은 [Git 자격 증명 및 풀 리퀘스트](#git-credentials)를, 지원 공급자와 작업은 [풀 리퀘스트 관리](#pull-request-management)를 참고하세요.

### <a name="git-limitations-memory"></a>메모리 제약

- Android와 iOS의 네이티브 Git은 JavaScript Git 엔진 밖에서 저장소 작업을 수행합니다. 브라우저 엔진의 메모리 제한이 모바일 Git의 고정 한도는 아닙니다.
- 네이티브 Git도 사용 가능한 메모리와 디스크 공간이 필요합니다. 큰 저장소나 pack 파일이 기기 리소스를 초과하면 작업이 실패하거나 운영 체제가 앱을 종료할 수 있습니다.
- 브라우저 Git은 JavaScript 메모리와 브라우저 저장소 한도의 제약을 받습니다. 큰 pack 파일은 많은 메모리가 필요하여 복제나 가져오기가 실패할 수 있습니다.

> 💡 **팁:** 큰 저장소에는 가능하면 얕은 복제를 사용하거나 저장소의 작은 부분으로 작업하세요.

### <a name="git-limitations-symlinks"></a>심볼릭 링크 호환성

- 브라우저 저장소와 편집기의 기기 파일 시스템 계층은 심볼릭 링크가 있는 저장소에 **에뮬레이트된 심볼릭 링크**를 사용합니다.
- 모바일 Git을 libgit2로 바꿔도 파일 시스템 제한이 사라지거나 실제 운영 체제 심볼릭 링크가 보장되지는 않습니다.
- 실제 링크를 기대하고 실행 중 대상 경로를 해석하는 빌드 도구, 패키지 관리자, 스크립트에서는 에뮬레이트된 링크가 다르게 동작할 수 있습니다.
- 실제 심볼릭 링크가 필요하면 이를 지원하는 파일 시스템과 권한을 가진 호스트의 원격 프로젝트를 사용하세요.

### <a name="git-limitations-cli"></a>대안으로 CLI 사용

큰 저장소 또는 호스트의 파일 시스템과 Git 도구가 필요한 작업에는 **Spck CLI를 통한 원격 프로젝트**를 사용하세요. Spck에서 편집하는 동안 **호스트의 Git 바이너리**로 Git 작업을 실행합니다.

- 저장소 작업은 모바일 기기나 브라우저 대신 호스트의 메모리와 디스크를 사용합니다.
- 심볼릭 링크는 호스트 운영 체제의 파일 시스템 지원과 권한을 따릅니다.
- 편집기 Git 컨트롤에 없는 명령은 호스트의 Git 도구를 사용하세요.

호스트 연결은 [Spck CLI 시작하기](./cli-start)를 참고하세요. 원격 프로젝트는 Spck 계정이 필요하며 요금제의 접근 한도가 적용됩니다. Lite의 구독 요건은 [원격 프로젝트](./editor-lite#remote-projects)를 참고하세요. 기기 저장소에 복제할 때는 계속 모바일 앱의 네이티브 Git 클라이언트를 사용합니다.

## <a name="git-related-guides"></a>관련 가이드

- [스크린 리더 지원(실험적)](./screen-reader-support): 접근 가능한 탐색, 소스 제어 컨트롤, 피드백.
- [Spck Editor Lite](./editor-lite#enhanced-git-integration): 일회성 앱 구매에 포함된 Git 도구.
- [Spck CLI 시작하기](./cli-start): 원격 프로젝트를 연결하여 호스트 Git 도구 사용.
