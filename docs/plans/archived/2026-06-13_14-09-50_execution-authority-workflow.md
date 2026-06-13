# Plan: 실행 권한 계층과 README 워크플로우 반영

## Status (상태)

archived

## Summary (요약)

이 계획은 `.project-context/`의 참조 권한을 작업 단계별로 명확히 하고, 계획 승인 후 구현 단계의 실행 기준을 공식 문서 중심으로 정리합니다.

또한 루트 `README.md`에 Intent-Anchored Development의 반복 흐름을 영어 노드 Mermaid 다이어그램으로 추가하고, 세션 체크포인트 업데이트 규칙을 강화합니다.

## Goal (목표)

- `.project-context/`를 실행 권한이 아닌 맥락 수집과 근거 보관 공간으로 명확히 정의합니다.
- 계획 작성 중 기본 참조 가능한 범위를 `.project-context/discussions/draft`와 `.project-context/discussions/open`으로 정합니다.
- `.project-context/reports/`는 특정 시점의 관찰과 근거이며 기본 참조 대상이 아님을 명시합니다.
- 최신 세션 파일 1개는 장기 작업 시작 시 기본 참조하되, 세션은 공식 기준이 아니라 인계 체크포인트임을 명시합니다.
- 루트 `README.md`에 논의, 승인, 계획, 구현, 검증, 드리프트 루프를 Mermaid로 표현합니다.

## Scope (작업 범위)

포함:

- `README.md`에 `Workflow` 또는 동등한 섹션 추가
- `README.md`에 영어 노드 Mermaid 다이어그램 추가
- `AGENTS.md`에 단계별 `.project-context/` 참조 규칙 추가
- `.project-context/README.md`에 실행 권한과 맥락 보관소의 차이 명시
- `.project-context/discussions/README.md`에 `draft/open/closed` 논의의 참조 의미 보강
- `.project-context/reports/README.md`에 보고서는 특정 시점의 근거이며 실행 기준이 아니라는 점 명시
- `.project-context/sessions/README.md`에 세션 업데이트 조건 강화
- `docs/plans/README.md`에 계획서가 승인 후 실행 기준을 충분히 흡수해야 한다는 원칙 보강

제외:

- 실제 파일 권한 또는 opencode tool permission 기반 접근 제어 구현
- 기존 보고서 전체 재작성
- 기존 세션 파일 전체 재작성
- 다국어 README 작성
- README 외 언어별 문서 생성

## Non-Goals (제외 목표)

- `.project-context/`를 삭제하거나 공식 문서 위치로 승격하지 않습니다.
- `.project-context/reports/`를 운영 기준 문서로 사용하지 않습니다.
- 세션 체크포인트를 계획서나 계약 문서의 대체물로 만들지 않습니다.
- 모든 작은 작업에 논의/계획 작성을 강제하지 않습니다.

## Assumptions (가정)

- 사용자는 논의 문서의 결론을 승인했습니다.
- 참조 제한은 실제 파일 접근 차단이 아니라 에이전트 작업 규칙입니다.
- 최신 세션 파일 1개는 context drift를 줄이기 위한 예외적 기본 참조 대상입니다.
- 보고서가 계속 필요한 운영 기준을 담고 있다면 보고서를 직접 참조하게 하지 않고 공식 문서로 승격해야 합니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_14-02-12_execution-authority-workflow.md`
- 관련 정책: `README.md`, `AGENTS.md`, `.project-context/README.md`, `docs/plans/README.md`

## Risks (리스크)

- 참조 제한 규칙이 너무 복잡하면 에이전트가 언제 멈춰야 하는지 혼란스러울 수 있습니다.
- 보고서 기본 참조 금지를 명확히 하지 않으면 과거 시점의 관찰이 현재 실행 기준처럼 사용될 수 있습니다.
- 최신 세션 파일 기본 참조는 유용하지만, 세션이 오래되거나 갱신되지 않으면 오히려 context drift를 키울 수 있습니다.
- Mermaid 다이어그램이 README 상단을 길게 만들 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] README workflow 반영
- [x] 참조 권한 계층 반영
- [x] reports 기본 참조 금지 반영
- [x] sessions 업데이트 강화
- [x] plans 실행 기준 흡수 원칙 반영
- [x] 검증

## Plan Tree (계획 트리)

- [x] 1. 착수 처리
- [x] 1.1. 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경
- [x] 2. `README.md` 갱신
- [x] 2.1. `Workflow` 섹션 위치 결정
- [x] 2.2. 영어 노드 Mermaid 다이어그램 추가
- [x] 2.3. `.project-context/`와 공식 실행 기준의 차이 요약
- [x] 3. `AGENTS.md` 갱신
- [x] 3.1. 단계별 기본 참조 가능 범위 추가
- [x] 3.2. 보고서 참조 금지와 승인 후 예외 참조 규칙 추가
- [x] 3.3. 최신 세션 파일 기본 참조와 세션의 권한 한계 명시
- [x] 4. `.project-context/` README 문서 갱신
- [x] 4.1. `.project-context/README.md`에 실행 권한 아님을 명시
- [x] 4.2. `.project-context/discussions/README.md`에 draft/open/closed 참조 의미 보강
- [x] 4.3. `.project-context/reports/README.md`에 보고서는 point-in-time evidence임을 명시
- [x] 4.4. `.project-context/sessions/README.md`에 세션 업데이트 조건 강화
- [x] 5. `docs/plans/README.md` 갱신
- [x] 5.1. 계획서는 승인 후 필요한 맥락을 충분히 흡수해야 한다는 원칙 추가
- [x] 6. 검증
- [x] 6.1. 경로와 상태 목록 확인
- [x] 6.2. Mermaid 코드 블록 렌더링 문법 확인
- [x] 6.3. `git diff`로 변경 범위 확인
- [x] 7. 완료 처리
- [x] 7.1. 체크리스트 완료 반영
- [x] 7.2. 계획서를 `docs/plans/archived/`로 이동하고 결과 기록

## Checklist (전체 체크리스트)

- [x] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done)
- [x] CL-002: `README.md`에 workflow 섹션과 Mermaid 다이어그램 추가 (done)
- [x] CL-003: `README.md`에 공식 실행 기준과 `.project-context/`의 차이 요약 (done)
- [x] CL-004: `AGENTS.md`에 단계별 기본 참조 가능 범위 추가 (done)
- [x] CL-005: `AGENTS.md`에 보고서 기본 참조 금지와 승인 후 예외 참조 규칙 추가 (done)
- [x] CL-006: `AGENTS.md`에 최신 세션 파일 기본 참조와 세션 권한 한계 추가 (done)
- [x] CL-007: `.project-context/README.md`에 실행 권한 아님을 명시 (done)
- [x] CL-008: `.project-context/discussions/README.md`에 draft/open/closed 참조 의미 보강 (done)
- [x] CL-009: `.project-context/reports/README.md`에 보고서는 특정 시점의 근거임을 명시 (done)
- [x] CL-010: `.project-context/sessions/README.md`에 세션 업데이트 조건 강화 (done)
- [x] CL-011: `docs/plans/README.md`에 계획서의 맥락 흡수 책임 추가 (done)
- [x] CL-012: 관련 경로와 상태 목록 확인 (done)
- [x] CL-013: Mermaid 문법 확인 (done)
- [x] CL-014: 최종 변경 범위 확인 (done)
- [x] CL-015: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done)

## Verification (검증)

- `README.md`에 Mermaid 코드 블록이 `flowchart TD` 형식으로 추가됐는지 확인합니다.
- `AGENTS.md`에 계획 작성 중, 계획 승인 후 구현 중, 예외 참조 규칙이 구분돼 있는지 확인합니다.
- `.project-context/reports/README.md`에 보고서가 실행 기준이 아니라 특정 시점의 근거라는 설명이 있는지 확인합니다.
- `.project-context/sessions/README.md`에 세션 업데이트 조건이 구체화됐는지 확인합니다.
- `docs/plans/README.md`에 계획서가 실행 기준에 필요한 맥락을 흡수해야 한다는 설명이 있는지 확인합니다.
- `git status --short`와 `git diff`로 의도한 문서만 변경됐는지 확인합니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

- 참조 권한 규칙이 과도하게 복잡하다고 판단되면 `AGENTS.md`에는 원칙만 남기고 세부 예외는 각 README로 이동합니다.
- Mermaid 다이어그램이 README 가독성을 해치면 텍스트 workflow로 대체합니다.
- 세션 업데이트 강화가 과도하면 장기 작업, 큰 작업 단위 종료, 중단 전으로 조건을 축소합니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 승인에 따라 논의 문서를 닫고 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `README.md`, `AGENTS.md`, `.project-context/README.md`, `.project-context/discussions/README.md`, `.project-context/reports/README.md`, `.project-context/sessions/README.md`, `docs/plans/README.md`에 실행 권한 계층과 참조 규칙을 반영했습니다.
- 2026-06-13: 검증 후 이 계획서를 `docs/plans/archived/`로 이동했습니다.

## Result (결과)

실행 권한 계층을 공식 문서에 반영했습니다. 계획 작성 중에는 `.project-context/discussions/draft`와 `.project-context/discussions/open`을 기본 참조할 수 있고, 계획 승인 후 구현 단계에서는 `PROJECT.md`, `AGENTS.md`, `docs/contracts/`, `docs/architectures/`, 승인된 `docs/plans/`를 기준으로 작업하도록 정리했습니다.

`.project-context/reports/`는 특정 시점의 관찰과 근거이며 기본 실행 기준이 아니라는 점을 명시했습니다. 최신 세션 파일 1개는 장기 작업 시작 시 기본 참조하되, 세션은 공식 요구사항이나 계획을 대체하지 않는 인계 체크포인트로 정의했습니다.

루트 `README.md`에는 영어 노드 Mermaid workflow를 추가해 논의, 승인, 계획, 구현, 검증, 드리프트 발견 시 되돌아가는 루프를 표현했습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_14-02-12_execution-authority-workflow.md`

영향:

- `README.md`
- `AGENTS.md`
- `.project-context/README.md`
- `.project-context/discussions/README.md`
- `.project-context/reports/README.md`
- `.project-context/sessions/README.md`
- `docs/plans/README.md`
