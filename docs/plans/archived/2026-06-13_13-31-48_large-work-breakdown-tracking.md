# Plan: 대형 작업 분할 관리 규칙 반영

## Status (상태)

archived

## Summary (요약)

이 계획은 대형 구현, 개편, 논의, 계획을 디렉토리 단위로 분할 관리하는 규칙을 공식 문서에 반영합니다. 일반 계획/논의는 기존처럼 상태 디렉토리 바로 아래 `.md` 파일로 두고, 대형 계획/논의는 상태 디렉토리 바로 아래 디렉토리와 `main-plan.md` 또는 `main-discussion.md`로 관리합니다.

## Goal (목표)

- 대형 계획/논의의 상위 문서와 하위 문서 관리 규칙을 명확히 합니다.
- 하위 문서 깊이를 1단계로 제한합니다.
- README 문서 목록 범위와 main 문서의 하위 문서 관리 책임을 명시합니다.
- opencode Todo와 계획서 체크리스트의 개념 차이를 문서화합니다.
- 간단한 작업은 논의/계획 없이 진행 가능함을 `AGENTS.md`에 명시합니다.

## Scope (작업 범위)

포함:

- `AGENTS.md`의 대형 작업, Todo, 간단한 작업 처리 규칙 갱신
- `docs/plans/README.md`의 대형 계획 디렉토리 구조와 Todo/체크리스트 관계 갱신
- `.project-context/discussions/README.md`의 대형 논의 디렉토리 구조와 README 목록 규칙 갱신
- 필요한 경우 현재 문서 목록 갱신

제외:

- 기존 완료 문서 전체의 역사적 경로 표현 일괄 수정
- 자동 문서 생성기 또는 링크 검증 도구 도입
- 실제 대형 계획/논의 샘플 디렉토리 생성
- opencode Todo 기능 동작 변경

## Non-Goals (제외 목표)

- 문서 상태명 체계를 다시 변경하지 않습니다.
- plans의 `scheduled|doing|archived`와 discussions의 `draft|open|closed` 상태명을 유지합니다.
- 대형 문서 아래 2단계 이상의 하위 문서 구조를 허용하지 않습니다.

## Assumptions (가정)

- 대형 계획/논의 디렉토리는 상태 디렉토리 바로 아래에 위치합니다.
- 대형 계획 디렉토리의 외부 상태는 `main-plan.md`의 상태를 따릅니다.
- 대형 논의 디렉토리의 외부 상태는 `main-discussion.md`의 상태를 따릅니다.
- 하위 문서의 상태는 대형 디렉토리 내부 상태 디렉토리를 따릅니다.
- README 목록은 상태 디렉토리 바로 아래 일반 문서와 대형 디렉토리까지만 나열합니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_13-17-01_large-work-breakdown-tracking.md`

## Risks (리스크)

- 대형 디렉토리 규칙이 길어지면 README가 복잡해질 수 있습니다.
- 하위 문서 상태와 main 문서 상태의 관계가 불명확하면 이동 시 혼란이 생길 수 있습니다.
- Todo와 체크리스트의 차이를 너무 엄격하게 쓰면 간단한 작업에도 문서화 부담이 생길 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] 문서 규칙 반영
- [x] Todo와 체크리스트 관계 명시
- [x] 문서 목록 규칙 갱신
- [x] 검증

## Plan Tree (계획 트리)

- [x] 1. 착수 처리
- [x] 1.1. 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경
- [x] 2. `AGENTS.md` 갱신
- [x] 2.1. 대형 계획/논의 디렉토리 규칙 추가
- [x] 2.2. Todo와 계획 체크리스트의 관계 추가
- [x] 2.3. 간단한 작업은 논의/계획 없이 진행 가능하다는 규칙 추가
- [x] 3. `docs/plans/README.md` 갱신
- [x] 3.1. 일반 계획과 대형 계획 구조 설명 추가
- [x] 3.2. 대형 계획 내부 상태 디렉토리와 `main-plan.md` 규칙 추가
- [x] 3.3. README 목록은 상위 계획까지만 나열한다는 규칙 추가
- [x] 3.4. Todo와 체크리스트의 관계 설명 추가
- [x] 4. `.project-context/discussions/README.md` 갱신
- [x] 4.1. 일반 논의와 대형 논의 구조 설명 추가
- [x] 4.2. 대형 논의 내부 상태 디렉토리와 `main-discussion.md` 규칙 추가
- [x] 4.3. README 목록은 상위 논의까지만 나열한다는 규칙 추가
- [x] 5. 검증
- [x] 5.1. 관련 경로와 상태명 검색
- [x] 5.2. `git status --short` 확인
- [x] 6. 완료 처리
- [x] 6.1. 체크리스트 완료 반영
- [x] 6.2. 계획서를 `docs/plans/archived/`로 이동하고 결과 기록

## Checklist (전체 체크리스트)

- [x] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done)
- [x] CL-002: `AGENTS.md`에 대형 작업 관리 규칙 추가 (done)
- [x] CL-003: `AGENTS.md`에 Todo와 계획 체크리스트 관계 추가 (done)
- [x] CL-004: `AGENTS.md`에 간단한 작업은 논의/계획 없이 진행 가능하다는 규칙 추가 (done)
- [x] CL-005: `docs/plans/README.md`에 대형 계획 구조 추가 (done)
- [x] CL-006: `docs/plans/README.md`에 README 목록과 main 문서 관리 규칙 추가 (done)
- [x] CL-007: `docs/plans/README.md`에 Todo와 체크리스트 관계 추가 (done)
- [x] CL-008: `.project-context/discussions/README.md`에 대형 논의 구조 추가 (done)
- [x] CL-009: `.project-context/discussions/README.md`에 README 목록과 main 문서 관리 규칙 추가 (done)
- [x] CL-010: 관련 경로와 상태명 검색으로 검증 (done)
- [x] CL-011: 최종 `git status --short` 확인 (done)
- [x] CL-012: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done)

## Verification (검증)

- `AGENTS.md`, `docs/plans/README.md`, `.project-context/discussions/README.md`에 대형 문서 구조 규칙이 반영됐는지 확인합니다.
- plans 상태명은 `scheduled`, `doing`, `archived`로 유지됐는지 확인합니다.
- discussions 상태명은 `draft`, `open`, `closed`로 유지됐는지 확인합니다.
- `sub/` 방식이 최종 권장안처럼 남아 있지 않은지 확인합니다.
- `git status --short`로 변경 범위를 확인합니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

- 규칙이 과도하게 복잡하다고 판단되면 대형 디렉토리 구조 문구를 제거하고 기존 단일 문서 규칙으로 되돌립니다.
- Todo와 체크리스트 관계 설명은 독립 규칙이므로 대형 디렉토리 구조와 분리해 유지할 수 있습니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 답변에 따라 `sub/` 방식 대신 대형 디렉토리와 내부 상태 디렉토리 방식을 채택했습니다.
- 2026-06-13: 논의 문서를 닫고 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `AGENTS.md`, `docs/plans/README.md`, `.project-context/discussions/README.md`에 대형 문서 구조와 Todo 관계 규칙을 반영했습니다.
- 2026-06-13: 검증 후 이 계획서를 `docs/plans/archived/`로 이동했습니다.

## Result (결과)

대형 계획/논의는 상태 디렉토리 바로 아래 디렉토리로 두고, `main-plan.md` 또는 `main-discussion.md`를 기준 문서로 사용하는 규칙을 반영했습니다. 하위 문서는 대형 디렉토리 내부 상태 디렉토리 아래 1단계까지만 허용하며, README 문서 목록은 상위 일반 문서와 대형 디렉토리까지만 나열하도록 정리했습니다.

opencode Todo와 계획서 체크리스트의 관계를 `AGENTS.md`와 `docs/plans/README.md`에 명시했습니다. 간단한 사용자 지시나 작은 작업은 논의/계획 없이 진행할 수 있다는 규칙도 `AGENTS.md`에 반영했습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_13-17-01_large-work-breakdown-tracking.md`

영향:

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`
- `docs/plans/archived/2026-06-13_13-31-48_large-work-breakdown-tracking.md`
