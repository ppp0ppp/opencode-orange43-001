# Use .opencode-context For Shared AI Context

작성일: 2026-06-06

## Context

사용자와 opencode는 큰 맥락의 논의, 보고서, 설계 결정, 세션 체크포인트를 Markdown으로 주고받는 것을 선호합니다. 기존 `docs/`는 제품/개발 문서와 섞일 수 있어 AI 작업 맥락 전용 위치로는 애매합니다.

## Decision

장기 AI 작업 맥락의 기준 디렉토리로 `.opencode-context/`를 사용합니다.

## Rationale

- opencode 전용 맥락임이 이름에 드러납니다.
- 일반 문서 디렉토리와 충돌하지 않습니다.
- 보고서, 결정 기록, 세션 체크포인트, 계약 문서를 하위 디렉토리로 분리할 수 있습니다.

## Consequences

- 관련 작업 전에는 `.opencode-context/` 문서를 먼저 확인해야 합니다.
- 계약 경계면 문서는 `.opencode-context/contracts/`를 우선 기준으로 삼습니다.
- 중요한 진행 상황은 `.opencode-context/sessions/`에 체크포인트로 남길 수 있습니다.
