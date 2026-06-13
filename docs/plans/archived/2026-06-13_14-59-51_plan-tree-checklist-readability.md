# Plan: Plan Tree와 체크리스트 가독성 규칙 반영

## Status (상태)

archived

## Summary (요약)

이 계획은 계획 문서의 `Plan Tree`를 tree glyph 기반 읽기용 구조 지도로 개선하고, `Checklist`가 실제 상태 추적의 source of truth임을 `docs/plans/README.md`에 반영합니다.

승인된 결론에 따라 `Plan Tree`에는 체크박스를 넣지 않고, 현재 작업 위치만 `[now]`로 표시합니다. `Checklist`에는 관련 `Plan Tree` ID를 `P:` 필드로 매핑합니다.

## Goal (목표)

- `Plan Tree`의 가독성을 개선합니다.
- `Plan Tree`와 `Checklist`의 책임을 명확히 분리합니다.
- `[now]` 표기와 `P:` 매핑 규칙을 문서화합니다.
- 계획 문서의 최소 필수 체크리스트 항목을 명시합니다.
- 논의 문서와 `AGENTS.md`에는 이번 규칙을 추가하지 않습니다.

## Scope (작업 범위)

포함:

- `docs/plans/README.md`의 `Plan Tree` 설명 보강
- `docs/plans/README.md`의 `Checklist` 설명 보강
- tree glyph 기반 `Plan Tree` 예시 추가
- `Checklist`의 `P:` 매핑 예시 추가
- 계획 문서 최소 필수 체크리스트 항목 명시
- `docs/plans/README.md` 문서 목록 갱신

제외:

- 기존 완료 계획 문서 전체 일괄 변환
- `.project-context/discussions/README.md` 수정
- `AGENTS.md` 수정
- 자동 포맷터 또는 검증 도구 구현

## Non-Goals (제외 목표)

- `Plan Tree`를 상태 추적 도구로 만들지 않습니다.
- 모든 논의 문서에 체크리스트를 추가하지 않습니다.
- 기존 archived 계획 문서의 과거 형식을 소급 변경하지 않습니다.

## Assumptions (가정)

- 사용자는 옵션 B를 승인했습니다.
- `[now]` 표기는 영어 `now`만 허용합니다.
- `P1/P1.1`과 `CL-001`의 매핑은 `Checklist` 쪽에 둡니다.
- 계획 문서 최소 체크리스트 항목은 필수로 둡니다.
- 이번 규칙은 `docs/plans/README.md`에 반영하고 `AGENTS.md`에는 추가하지 않습니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_14-43-44_plan-tree-checklist-readability.md`

## Risks (리스크)

- `Plan Tree`의 `[now]`와 `Checklist`의 `(now doing)`이 달라질 수 있습니다.
- tree glyph를 수동으로 관리하면서 문자가 깨질 수 있습니다.
- 최소 체크리스트 항목이 작은 계획에는 다소 무겁게 느껴질 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] README 규칙 보강
- [x] 예시 추가
- [x] 계획 문서 목록 갱신
- [x] 검증
- [x] 완료 처리

## Plan Tree (계획 트리)

```text
P1. 착수 처리
├─ P1.1. 계획서를 `doing`으로 이동
└─ P1.2. `docs/plans/README.md` 목록 갱신

P2. `docs/plans/README.md` 갱신
├─ P2.1. `Plan Tree` 규칙 보강
├─ P2.2. tree glyph 예시 추가
├─ P2.3. `Checklist` source of truth 규칙 보강
└─ P2.4. `P:` 매핑과 최소 필수 체크리스트 예시 추가

P3. 검증과 완료 처리
├─ P3.1. 변경 문서와 상태 목록 확인
├─ P3.2. `git diff`로 변경 범위 확인
└─ P3.3. 계획서를 `archived`로 이동하고 결과 기록
```

## Checklist (전체 체크리스트)

- [x] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done, P: P1.1)
- [x] CL-002: `docs/plans/README.md` 문서 목록을 `scheduled`에서 `doing`으로 갱신 (done, P: P1.2)
- [x] CL-003: `docs/plans/README.md`에 `Plan Tree` 규칙을 보강 (done, P: P2.1)
- [x] CL-004: `docs/plans/README.md`에 tree glyph 예시를 추가 (done, P: P2.2)
- [x] CL-005: `docs/plans/README.md`에 `Checklist` source of truth 규칙을 보강 (done, P: P2.3)
- [x] CL-006: `docs/plans/README.md`에 `P:` 매핑과 최소 필수 체크리스트 예시를 추가 (done, P: P2.4)
- [x] CL-007: 변경 문서와 상태 목록을 확인 (done, P: P3.1)
- [x] CL-008: `git diff`로 변경 범위를 확인 (done, P: P3.2)
- [x] CL-009: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done, P: P3.3)

## Verification (검증)

- `docs/plans/README.md`에 `Plan Tree`는 체크박스 없는 읽기용 지도라는 설명이 있는지 확인합니다.
- `docs/plans/README.md`에 `[now]`는 영어 `now`만 허용한다는 설명이 있는지 확인합니다.
- `docs/plans/README.md`에 `Checklist`가 source of truth라는 설명이 있는지 확인합니다.
- `docs/plans/README.md`에 `P:` 매핑 예시가 있는지 확인합니다.
- `docs/plans/README.md`에 최소 필수 체크리스트 항목이 있는지 확인합니다.
- `git status --short`와 `git diff`로 변경 범위를 확인합니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

- tree glyph 예시가 과하게 복잡하면 `P1/P1.1` flat list 예시로 되돌립니다.
- 최소 필수 체크리스트가 과하다고 판단되면 필수 항목을 강한 권장 예시로 낮춥니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 승인에 따라 논의 문서를 닫고 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `docs/plans/README.md`에 Plan Tree 형식, `[now]`, `P:` 매핑, 필수 체크리스트 항목을 반영했습니다.
- 2026-06-13: 검증 후 이 계획서를 `docs/plans/archived/`로 이동했습니다.

## Result (결과)

`docs/plans/README.md`에 Plan Tree와 Checklist의 책임 분리 규칙을 반영했습니다. Plan Tree는 체크박스 없는 tree glyph 기반 읽기용 지도로 정의했고, `[now]`는 영어 표기만 허용하며 한 번에 하나만 유지하도록 했습니다.

Checklist는 실제 상태 추적의 source of truth로 정의했고, 관련 Plan Tree ID를 `P:` 필드로 매핑하는 예시와 필수 체크리스트 최소 항목을 추가했습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_14-43-44_plan-tree-checklist-readability.md`

영향:

- `docs/plans/README.md`
