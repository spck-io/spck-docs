# 편집기 임베드

Spck Editor를 iframe에 넣어 편집 가능한 예제, 튜토리얼, 코드 도구를 만들 수 있습니다. `SpckEditor` 래퍼는 `postMessage`와 `MessageChannel`로 iframe과 통신합니다.

## <a name="screen-reader-support"></a>스크린 리더 지원(실험적)

접근성 기능과 현재 제한은 [스크린 리더 지원(실험적)](./screen-reader-support#screen-reader-limitations)을 참고하세요. 임베디드 편집기는 모바일 스크린 리더 편집 모드를 자동으로 활성화하지 않습니다.

설정, 프로젝트와 파일, 편집기 옵션, 이벤트 및 문제 해결은 [전체 API 참조(영어)](/en/editor-embed)를 참고하세요. 소스 코드와 TypeScript 선언은 [spckio/spck-embed](https://github.com/spckio/spck-embed)에 있습니다.
