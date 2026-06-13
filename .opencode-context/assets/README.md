# Assets

작업 중 계속 참조할 보존 자료를 두는 공간입니다.

## Purpose

- 보고서, 논의, 공식 문서에서 계속 참조할 이미지, 다이어그램, 샘플 문서를 보관합니다.
- `.opencode-context/inbox/`의 임시 원자료 중 보존 가치가 있는 파일을 정리해 승격합니다.

## Policy

- 커밋 가능한 자료만 둡니다.
- 민감정보, 개인정보, 토큰, 내부 URL은 제거하거나 마스킹합니다.
- 파일을 참조하는 보고서, 논의, 공식 문서에는 상대 경로를 함께 남깁니다.
- 제품/사용자/개발자 공식 문서로 승격된 자료는 `docs/`로 옮깁니다.

## Naming

짧은 kebab-case 이름을 권장합니다.

```text
.opencode-context/assets/
  auth-flow-diagram.png
  failing-screen-login.png
```
