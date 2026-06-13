# Plans (계획서)

프로젝트의 공식 계획 문서를 두는 위치입니다.

계획 문서는 실행할 작업의 범위, 체크리스트, 진행 상태, 검증 방법, 영향 문서를 추적합니다. 여러 계획이 동시에 진행될 수 있지만, 서로 영향을 주는 경우 의존성을 명시해야 합니다.

## Status Directories (상태 디렉토리)

- `scheduled/`: 아직 미승인인 계획서 또는 승인됐지만 아직 착수하지 않은 계획서
- `doing/`: 실행 중인 계획서
- `archived/`: 모든 항목이 완료되었거나 명시적으로 중단 처리된 계획서

계획서의 디렉토리 상태와 본문 `Status (상태)`는 항상 일치해야 합니다. 상태 이동 시 파일명은 바꾸지 않고 최초 생성 시각을 유지합니다.

## Naming (이름 규칙)

계획 문서는 상태 이동과 시간 추적성이 중요하므로 최초 생성 시각을 기준으로 다음 형식을 사용합니다.

```text
YYYY-MM-DD_HH-MM-SS_detail-title.md
```

대형 계획은 상태 디렉토리 바로 아래에 다음 형식의 디렉토리로 둡니다.

```text
YYYY-MM-DD_HH-MM-SS_detail-title/
```

대형 계획 디렉토리는 `main-plan.md`를 기준 문서로 사용합니다. 대형 계획 디렉토리의 외부 상태는 `main-plan.md`의 `Status (상태)`를 따릅니다.

## Large Plans (대형 계획)

대형 계획은 다음 구조를 사용합니다.

```text
docs/plans/doing/2026-06-13_13-17-01_large-work/
  main-plan.md
  scheduled/
    2026-06-13_13-20-00_sub-plan-a.md
  doing/
    2026-06-13_13-25-00_sub-plan-b.md
  archived/
    2026-06-13_13-30-00_sub-plan-c.md
```

- 일반 계획은 상태 디렉토리 바로 아래 `.md` 파일로 둡니다.
- 대형 계획은 상태 디렉토리 바로 아래 디렉토리로 둡니다.
- 대형 계획의 내부 상태 디렉토리는 `scheduled/`, `doing/`, `archived/`만 사용합니다.
- 하위 계획의 상태는 대형 계획 내부 상태 디렉토리와 본문 `Status (상태)`를 따릅니다.
- 하위 계획은 한 단계만 허용하며 하위 계획 아래에 다시 하위 계획 디렉토리를 만들지 않습니다.
- 하위 계획 목록과 진행 관리는 `main-plan.md`에서 합니다.
- README 문서 목록은 상태 디렉토리 바로 아래의 일반 계획과 대형 계획 디렉토리까지만 나열합니다.

## Checklist States (체크리스트 상태)

- `done`: 완료
- `now doing`: 현재 진행 중
- `pending`: 대기
- `aborted`: 중단 또는 폐기

체크리스트 항목은 다음 형식을 사용합니다.

```md
- [ ] CL-001: 항목 설명 (pending)
- [ ] CL-002: 항목 설명 (now doing)
- [x] CL-003: 항목 설명 (done)
- [ ] CL-004: 항목 설명 (aborted)
```

## Todo Relationship (Todo와 체크리스트 관계)

opencode Todo는 현재 세션 또는 현재 작업 턴의 최소 실행 단위입니다. 계획서의 `Checklist (전체 체크리스트)`는 문서로 보존되는 계획 추적 단위입니다.

- 하나의 Todo 목록이 하나의 계획서 전체를 처리할 수 있습니다.
- 하나의 Todo 목록이 여러 체크리스트 항목을 처리할 수 있습니다.
- 하나의 Todo 목록이 단일 체크리스트 항목을 처리할 수 있습니다.
- 단일 체크리스트 항목을 여러 Todo 목록으로 나누어 처리할 수 있습니다.
- 간단한 작업은 계획서 없이 Todo만 사용하거나 Todo 없이 바로 진행할 수 있습니다.

## Required Sections (필수 섹션)

계획 문서는 아래 섹션 순서를 고정합니다. 특정 문서에서 필요하지 않은 섹션도 삭제하지 않고 `사용하지 않음` 또는 `현재 없음`으로 명시합니다.

`Status (상태)`:

- 현재 계획서의 상태를 적습니다.
- 허용 값은 `scheduled`, `doing`, `archived`입니다.

`Summary (요약)`:

- 계획의 목적과 핵심 작업을 2~5문장으로 요약합니다.

`Goal (목표)`:

- 완료되면 무엇이 달라져야 하는지 적습니다.
- 성공 기준이 명확하면 함께 적습니다.

`Scope (작업 범위)`:

- 본 계획이 포함하는 작업과 제외하는 작업을 적습니다.

`Non-Goals (제외 목표)`:

- 이번 계획에서 하지 않을 일을 적습니다.

`Assumptions (가정)`:

- 계획이 성립하기 위해 참이라고 보는 조건을 적습니다.

`Dependencies (의존성)`:

- 다른 계획, 논의, 문서, 코드 변경과의 의존성을 적습니다.

`Risks (리스크)`:

- 기술적, 운영적, 문서 정합성, 일정 리스크를 적습니다.

`Plan Ground (계획 기반 체크리스트)`:

- 계획 전체를 일반 분류별 체크리스트로 정리합니다.

`Plan Tree (계획 트리)`:

- 계획을 단계적으로 표현합니다.
- 선후관계, 하위 작업, 블로커를 드러냅니다.

`Checklist (전체 체크리스트)`:

- 모든 체크리스트 항목을 `CL-001` 형식으로 모읍니다.
- 각 항목에는 체크박스와 상태 값을 함께 둡니다.

`Verification (검증)`:

- 계획 완료를 어떻게 확인할지 적습니다.

`Rollback Or Abort Plan (롤백 또는 중단 계획)`:

- 계획을 중단하거나 되돌려야 할 조건과 처리 방식을 적습니다.

`Progress Notes (진행 메모)`:

- 진행 중 발견한 중요한 사실과 상태 변경을 적습니다.

`Result (결과)`:

- `archived` 상태로 이동할 때 최종 결과를 적습니다.

`References (근거 및 영향 문서)`:

- 계획의 근거가 되는 문서와 영향을 받는 문서를 적습니다.

## Documents (문서 목록)

Scheduled:

- 현재 없음

Doing:

- 현재 없음

Archived:

- `docs/plans/archived/2026-06-13_11-28-02_docs-context-restructure.md`: docs 및 `.opencode-context` 문서 구조 재조정
- `docs/plans/archived/2026-06-13_12-18-13_context-directory-rename.md`: context 디렉토리 이름 변경
- `docs/plans/archived/2026-06-13_12-55-02_path-reference-style.md`: 문서 경로 표기 방식 표준화
- `docs/plans/archived/2026-06-13_13-31-48_large-work-breakdown-tracking.md`: 대형 작업 분할 관리 규칙 반영
