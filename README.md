# opencode Defaults Template

개인/팀용 opencode 로컬 기본 설정 템플릿입니다.

## Included

- `opencode.json`: 프로젝트 로컬 opencode 설정
- `AGENTS.md`: 공통 assistant 지시문
- `PROJECT.md`: 사용자가 미리 채우는 프로젝트 목표, 환경, 스택, 개발 철학
- `.opencode/skills/`: 로컬 skill
- `.opencode/plugins/`: 로컬 plugin
- `.opencode-context/`: 보고서, 논의, 의사결정, 세션 체크포인트, 계약 문서

## Project Setup

새 프로젝트에 이 템플릿을 적용할 때는 `PROJECT.md`를 먼저 채웁니다.

필수로 정하기 어려운 항목은 `미정`으로 남기고, 작업자가 추측하면 안 되는 항목은 `Open Questions (열린 질문)`에 적습니다.

## Bootstrap

새 환경으로 이식할 때는 아래 문서를 먼저 확인합니다.

- `.opencode-context/reports/003-bootstrap-installation-guide.md`
- `.opencode-context/reports/004-oh-my-opencode-slim-adoption.md`
- `.opencode-context/reports/005-oh-my-opencode-slim-diff.md`
- `.opencode-context/reports/006-slim-absorption-branch.md`

설정 변경 후에는 opencode를 재시작해야 합니다.
