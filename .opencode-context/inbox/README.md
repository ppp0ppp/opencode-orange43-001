# Inbox

사용자가 opencode 하네스/에이전트에 넘기는 외부 입력을 임시로 두는 공간입니다.

## Purpose

- 디버깅용 스크린샷, 이미지, PDF, 로그, 텍스트 덤프를 임시 저장합니다.
- 아직 정리되지 않은 원자료를 작업 세션에서 참조합니다.
- VLM이 가능한 모델을 사용할 때 `opencode run --file` 첨부 입력으로 사용할 수 있습니다.

## Policy

- 이 디렉토리의 실제 입력 파일은 기본적으로 git에 커밋하지 않습니다.
- 민감정보, 토큰, 개인정보, 내부 URL이 포함될 수 있으므로 외부 모델 전송 전에 확인합니다.
- 장기 보존할 자료는 필요한 민감정보를 제거한 뒤 `.opencode-context/assets/`로 승격합니다.
- 공식 사용자/개발자 문서가 된 자료는 `docs/`로 옮깁니다.

## Suggested Layout

날짜별 하위 디렉토리를 권장합니다.

```text
.opencode-context/inbox/
  2026-06-07/
    login-error.png
    api-response.txt
```

## opencode Attachment Example

```bash
opencode run --file .opencode-context/inbox/2026-06-07/login-error.png "이 화면 문제를 분석해줘"
```

이미지/PDF가 실제 vision 입력으로 처리되는지는 사용하는 provider/model의 멀티모달 지원 여부에 따릅니다.
