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

## 환경 설정

환경은 3단계로 나누어 준비합니다. 자세한 설치 절차는 `.opencode-context/reports/003-bootstrap-installation-guide.md`를 기준으로 확인합니다.

### 1. 타겟 OS 실행자 준비

사용할 OS에 맞게 명령 실행자와 기본 도구를 먼저 준비합니다.

예: shell, Git, 패키지 매니저, Docker, 언어별 버전 관리자, PATH 설정.

### 2. opencode 도구 실행 환경 준비

opencode와 이 템플릿에 포함된 도구가 필요로 하는 실행자를 준비합니다.

현재 템플릿 기준 핵심 항목은 opencode CLI, Git, graphify CLI입니다. graphify CLI 설치에는 Python 3.10 이상과 `uv` 또는 `pipx`를 사용할 수 있습니다. 단, 여기서의 `uv`는 graphify 설치 수단일 뿐 개발 타겟의 필수 런타임이 아닙니다.

현재 포함된 구성은 `opencode.json`, `AGENTS.md`, `.opencode/skills/`, `.opencode/plugins/graphify.js`, `.opencode/agents/oracle-review.md`입니다. git hook과 MCP 서버는 기본 활성화하지 않습니다.

### 3. 개발 타겟 환경 준비

실제 앱의 언어, 버전, 프레임워크, 런타임, DB, 테스트 도구는 `PROJECT.md`에 적습니다.

예: Python/FastAPI/LangGraph, Vite/TypeScript, Next.js, .NET, 또는 여러 앱이 묶인 복합 환경.

스택 선택이나 복합 앱 구조가 아직 뒤집힐 수 있으면 `.opencode-context/discussions/`에 논의 파일을 먼저 만들고, 확정된 내용만 `PROJECT.md`와 필요 시 `decisions/`에 반영합니다.

## Bootstrap

새 환경으로 이식할 때는 아래 문서를 먼저 확인합니다.

- `.opencode-context/reports/003-bootstrap-installation-guide.md`
- `.opencode-context/reports/004-oh-my-opencode-slim-adoption.md`
- `.opencode-context/reports/005-oh-my-opencode-slim-diff.md`
- `.opencode-context/reports/006-slim-absorption-branch.md`

설정 변경 후에는 opencode를 재시작해야 합니다.
