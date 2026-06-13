# Plans (계획서)

프로젝트의 공식 계획 문서를 두는 위치입니다.

계획 문서는 실행할 작업의 범위, 체크리스트, 진행 상태, 검증 방법, 영향 문서를 추적합니다. 여러 계획이 동시에 진행될 수 있지만, 서로 영향을 주는 경우 의존성을 명시해야 합니다.

계획서가 승인된 뒤 일반 구현 작업은 승인된 계획서와 공식 문서를 기준으로 진행합니다. 계획 수립 중 `.project-context/`에서 확인한 필요한 맥락은 계획서나 관련 공식 문서로 흡수되어 있어야 합니다.

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
- [ ] CL-001: 항목 설명 (pending, P: P1.1)
- [ ] CL-002: 항목 설명 (now doing, P: P2.1)
- [x] CL-003: 항목 설명 (done, P: P3.1)
- [ ] CL-004: 항목 설명 (aborted, P: P4.1)
```

## Plan Tree Format (계획 트리 형식)

`Plan Tree (계획 트리)`는 작업 구조와 현재 위치를 보여주는 읽기용 지도입니다. 실제 진행 상태의 기준은 `Checklist (전체 체크리스트)`입니다.

- `Plan Tree`에는 체크박스를 넣지 않습니다.
- `Plan Tree`는 fenced `text` 코드 블록에 작성합니다.
- 상위 항목은 `P1`, `P2`, `P3` 형식을 사용합니다.
- 하위 항목은 `P1.1`, `P1.2` 형식을 사용합니다.
- 기본 깊이는 2단계이며, 필요한 경우 `P1.1.1`까지 허용합니다.
- 4단계 이상이 필요하면 대형 계획의 하위 계획으로 분리하는 것을 우선 검토합니다.
- tree glyph인 `├─`, `└─`, `│`를 사용해 시각적으로 구분할 수 있습니다.
- 현재 작업 중인 항목은 선택적으로 `[now]`를 붙입니다.
- `[now]`는 한 번에 하나만 유지하고, `[현재]` 같은 번역 표기는 사용하지 않습니다.
- 완료, 대기, 중단 상태는 `Checklist`에서 관리합니다.

예시:

```text
P1. 착수 처리
├─ P1.1. 계획서를 `doing`으로 이동
└─ P1.2. 상태와 README 목록 갱신

P2. README 갱신 [now]
├─ P2.1. Workflow 섹션 추가
├─ P2.2. Mermaid 다이어그램 추가
└─ P2.3. 실행 권한 계층 요약

P3. 검증과 완료 처리
├─ P3.1. 변경 문서와 상태 목록 확인
└─ P3.2. 계획서를 `archived`로 이동하고 결과 기록
```

## Required Checklist Items (필수 체크리스트 항목)

모든 계획 문서는 최소한 착수, 변경 수행, 검증, 완료 처리 항목을 포함해야 합니다. 변경 수행 항목은 실제 계획 범위에 맞게 여러 `CL` 항목으로 세분화합니다.

`Checklist` 항목은 관련 `Plan Tree` ID가 있으면 `P:` 필드로 매핑합니다. 여러 항목에 걸치면 `P: P2.1, P2.2`처럼 적습니다. 직접 연결되는 `Plan Tree` 항목이 없으면 `P:` 필드는 생략할 수 있습니다.

최소 예시:

```md
- [ ] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (pending, P: P1.1)
- [ ] CL-002: 계획 범위의 변경을 수행 (pending, P: P2)
- [ ] CL-003: 관련 문서, 상태 목록, 변경 범위를 검증 (pending, P: P3.1)
- [ ] CL-004: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (pending, P: P3.2)
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

- 계획을 단계적으로 표현하는 읽기용 지도입니다.
- 체크박스를 넣지 않고 `Plan Tree Format (계획 트리 형식)`을 따릅니다.
- 현재 작업 중인 항목은 `[now]`로 표시할 수 있습니다.

`Checklist (전체 체크리스트)`:

- 모든 체크리스트 항목을 `CL-001` 형식으로 모읍니다.
- 각 항목에는 체크박스와 상태 값을 함께 둡니다.
- 실제 진행 상태 추적의 기준입니다.
- 관련 `Plan Tree` 항목이 있으면 `P:` 필드로 매핑합니다.
- `Required Checklist Items (필수 체크리스트 항목)`의 최소 항목을 포함합니다.

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
- `.project-context/` 문서를 근거로 삼는 경우, 구현 단계에서 계속 필요한 결론은 계획서 본문이나 공식 문서에 흡수합니다.
- 계획 중 웹 접근을 사용했다면 항상 URL, 공식/비공식 여부, 확인 목적을 짧게 기록합니다.
- 비공식 출처는 사용자 승인 여부나 공식 출처가 아님을 별도로 표시합니다.

웹 확인 기록 예시:

```md
웹 확인:

- 공식: `https://opencode.ai/config.json`: opencode config schema 확인
- 비공식: `https://example.com/blog/post`: 사례 참고, 사용자 승인 후 참고
```

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
- `docs/plans/archived/2026-06-13_14-09-50_execution-authority-workflow.md`: 실행 권한 계층과 README 워크플로우 반영
- `docs/plans/archived/2026-06-13_14-59-51_plan-tree-checklist-readability.md`: Plan Tree와 체크리스트 가독성 규칙 반영
- `docs/plans/archived/2026-06-13_15-47-57_planning-web-access-policy.md`: 논의/계획 단계 웹 접근 정책 반영
