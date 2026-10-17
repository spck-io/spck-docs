# <a name="editor-lite"></a>Spck Editor Lite

## <a name="overview"></a>개요

Spck Editor Lite는 구독 없이 프리미엄 편집 기능을 잠금 해제하는 Spck Editor의 일회성 구매 버전입니다. Android와 iOS 모두에서 별도 앱으로 제공됩니다.

Lite에는 무료 버전의 모든 기능에 더해 다음이 포함됩니다:

- **Predictive Keyboard** -- 추가 키보드의 문맥 인식 기호 제안
- **사용자 정의 스니펫** -- 탭 스톱 플레이스홀더가 있는 사용자 정의 코드 템플릿
- **Neon 테마** -- 독점 에디터 테마
- **향상된 Git 통합** -- 커밋의 변경 파일 목록 및 읽기 전용 diff

이러한 기능은 Gold 또는 Supporter 구독이 활성화된 Spck Editor 정식 버전에서도 사용할 수 있습니다. Lite 앱은 동일한 기능을 일회성 구매로 제공합니다.

## <a name="remote-projects"></a>원격 프로젝트

Lite는 Spck CLI를 통해 데스크톱이나 공개 VM에 있는 프로젝트를 편집할 수 있습니다. 원격 프로젝트에는 Lite 일회성 구매와 별도로 **Spck 계정과 활성 Spck 구독**이 필요합니다. 구독은 Spck 서버의 지속적인 호스팅, 운영 및 유지 관리 비용을 지원합니다. 포함된 로컬 편집 및 Git 도구는 구독 없이 계속 사용할 수 있습니다.

[Spck CLI](./cli-start) · [Spck](https://spck.io/pricing)

## <a name="predictive-keyboard"></a>Predictive Keyboard

Predictive Keyboard는 표준 추가 키보드를 문맥 인식 기호 키 행으로 대체합니다. 키를 길게 눌러 메뉴에서 선택하는 대신, 파일 내 커서 위치에 따라 가장 가능성 높은 기호가 직접 표시됩니다.

### 작동 방식

예측은 언어별로 구축된 통계적 빈도 테이블에서 생성됩니다. 커서가 이동하면 키보드는 실제 코드에서 해당 유형의 위치에 각 기호가 얼마나 자주 나타나는지에 따라 기호를 재정렬합니다. 지원 언어에는 JavaScript, TypeScript, Python, HTML, CSS, JSON, Java, C++, Go, Markdown 및 일반 텍스트가 포함됩니다.

### 활성화 또는 비활성화

`Settings > Touch > Predictive Keyboard`에서 기능을 전환합니다. Lite에서는 Predictive Keyboard가 기본적으로 활성화되어 있습니다. 비활성화하면 표준 추가 키보드로 복원됩니다.

> Predictive Keyboard는 터치 기기에서만 사용할 수 있습니다. 물리적 키보드를 사용하거나 외부 키보드가 연결된 태블릿 모드에서는 표시되지 않습니다.

## <a name="custom-snippets"></a>사용자 정의 스니펫

사용자 정의 스니펫을 사용하면 입력 중 자동 완성 목록에 표시되는 재사용 가능한 코드 템플릿을 만들 수 있습니다. 각 스니펫은 특정 언어에 연결되므로 JavaScript 스니펫이 Python 파일에 표시되지 않습니다.

### 스니펫 만들기

1. `Settings > Editor > Custom Snippets` 열기
2. 언어 선택 (예: JavaScript, Python, HTML)
3. **스니펫 추가** 탭
4. **트리거** 입력 -- 스니펫을 호출하기 위해 입력하는 약어
5. **본문** 입력 -- 삽입될 코드

### 탭 스톱과 플레이스홀더

스니펫은 탭 스톱을 지원하여 삽입 후 커서가 편집 가능한 위치 사이를 이동합니다:

- `$1`, `$2`, `$3` -- 이동 순서대로 번호가 매겨진 탭 스톱
- `$0` -- 모든 탭 스톱 이후의 최종 커서 위치
- `${1:defaultText}` -- 쉽게 교체할 수 있도록 미리 선택된 플레이스홀더 텍스트가 있는 탭 스톱

예시 -- JavaScript `for` 루프 스니펫:

**트리거:** `forloop`

**본문:**
```
for (let ${1:i} = 0; ${1:i} < ${2:array}.length; ${1:i}++) {
  $0
}
```

`forloop`을 입력하고 자동 완성에서 선택하면 전체 루프가 삽입됩니다. Tab 키를 눌러 `i`, `array`, 루프 본문 사이를 이동합니다.

### 가져오기 및 내보내기

모든 스니펫을 파일로 내보내고 다른 기기에서 가져올 수 있습니다. 이 기능은 휴대폰 간에 스니펫 컬렉션을 공유하거나 설정을 백업하는 데 유용합니다.

## <a name="neon-theme"></a>Neon 테마

Lite에는 **Neon** 에디터 테마가 포함되어 있습니다. 선명한 강조 색상의 다크 테마입니다. Lite에서 기본 테마로 설정되어 있으며 `Settings > Appearance > Theme`에서 언제든지 변경할 수 있습니다.

## <a name="enhanced-git-integration"></a>향상된 Git 통합

Git 패널의 **History** 탭을 열고 커밋을 선택하면 추가, 수정, 삭제된 파일을 볼 수 있습니다. 파일을 선택하면 첫 번째 부모 커밋과 비교하는 읽기 전용 diff가 열립니다. 첫 커밋은 빈 트리와 비교합니다. 뷰어는 커밋에 저장된 버전을 사용하므로 커밋되지 않은 편집은 diff에 영향을 주지 않습니다. 바이너리 파일은 텍스트 diff로 표시할 수 없습니다.

향상된 Git 통합은 Spck Lite와 Spck for NodeJS 터미널 평생 이용권에 영구적으로 포함됩니다. 활성 Supporter, Gold 또는 Node 구독에도 포함됩니다. 전체 앱은 로그인이 필요하며 Lite는 필요하지 않습니다. [향상된 Git 통합](./editor#enhanced-git-integration).

## <a name="comparison"></a>기능 비교

| 기능 | 무료 | Lite (일회성 구매) | 정식 (구독) |
| --- | :---: | :---: | :---: |
| 코드 편집 및 구문 강조 | 예 | 예 | 예 |
| Git 연동 | 예 | 예 | 예 |
| 향상된 Git 통합 | -- | 예 | Supporter / Gold / Node |
| 추가 키보드 | 예 | 예 | 예 |
| 터치 키보드 및 커서 | 예 | 예 | 예 |
| 프로젝트 미리보기 | 예 | 예 | 예 |
| Predictive Keyboard | -- | 예 | Gold / Supporter |
| 사용자 정의 스니펫 | -- | 예 | Gold |
| Neon 테마 | -- | 예 | -- |
| AI 어시스턴트 | -- | -- | 예 |
| 클라우드 동기화 | -- | -- | 예 |
| Labs / 커뮤니티 프로젝트 | -- | -- | 예 |
