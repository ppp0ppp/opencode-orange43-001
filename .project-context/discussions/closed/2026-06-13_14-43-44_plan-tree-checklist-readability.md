# Discussion: Plan Tree와 체크리스트 가독성 개선

## Status (상태)

closed

## Summary (요약)

이 논의는 계획 문서의 `Plan Tree (계획 트리)` 가독성을 개선하고, 논의/계획 문서의 체크리스트 예시 또는 최소 필수 항목을 강화하는 방안을 정리합니다.

최종 결론은 `Plan Tree`를 체크박스 없는 읽기용 구조 지도로 두고, `├`, `└`, `│` 같은 tree glyph를 사용해 시각적으로 구분하는 것입니다. 실제 상태 추적은 `Checklist (전체 체크리스트)`가 담당하며, `Plan Tree`에는 현재 작업 위치만 선택적으로 `[now]`로 표시합니다.

## Background (배경)

현재 계획 문서는 `Plan Ground`, `Plan Tree`, `Checklist`를 모두 포함합니다. 이 구조는 역할이 분리되어 있지만, 기존 `Plan Tree` 예시는 평평한 체크리스트 형태에 가까워 대형 계획에서 계층과 현재 위치를 한눈에 보기 어렵습니다.

사용자는 다음 개선 필요를 제기했습니다.

- 계획서 트리 구조의 가독성 개선
- 논의/계획 문서 체크리스트의 필수 목록 지정 또는 예시 강화

이후 논의에서 `├`, `└`, `│` 같은 tree glyph를 사용해 트리 구조를 더 시각적으로 분리하고, 트리에는 체크박스를 넣지 않되 현재 작업 중인 위치 정도는 표시하는 방향이 선호되었습니다.

## Context (맥락)

현재 `docs/plans/README.md`는 다음 역할을 정의합니다.

- `Plan Ground`: 계획 전체를 일반 분류별 체크리스트로 정리
- `Plan Tree`: 계획을 단계적으로 표현하고 선후관계, 하위 작업, 블로커를 드러냄
- `Checklist`: 모든 체크리스트 항목을 `CL-001` 형식으로 모으고 체크박스와 상태 값을 함께 둠

이 역할 구분은 유지하는 편이 좋습니다. 다만 `Plan Tree`의 예시와 규칙이 충분히 구체적이지 않아, 실제 작성 시 체크박스와 상태 추적까지 섞이는 문제가 생길 수 있습니다.

## Scope (범위)

포함:

- `Plan Tree`의 권장 표현 방식 정의
- `Plan Tree`와 `Checklist`의 책임 분리
- `[now]` 표시 규칙 정의
- 계획 문서의 최소 필수 체크리스트 예시 강화
- 논의 문서 체크리스트 적용 여부 검토
- 확정 시 반영 대상 문서 후보 정리

제외:

- 기존 완료된 계획 문서 전체의 일괄 변환
- 모든 논의 문서에 체크리스트 섹션을 필수 추가하는 작업
- 자동 문서 포맷터 또는 검증 도구 구현
- 현재 열린 브랜치 전략 논의 문서 수정

## Constraints (제약)

- `Plan Tree`는 사람이 빠르게 구조를 읽는 데 초점을 둡니다.
- 실제 진행 상태의 기준은 `Checklist`여야 합니다.
- `Plan Tree`와 `Checklist`가 같은 상태를 중복 추적하면 document drift가 생길 수 있습니다.
- tree glyph는 Markdown 렌더링에서 깨지지 않도록 fenced `text` 코드 블록 안에 둡니다.
- `[now]`는 현재 위치 표시용이며, 완료/대기/중단 상태를 대체하지 않습니다.
- 작은 계획 문서에 과한 형식을 강제하면 문서화 비용이 커질 수 있습니다.

## Analysis (분석)

기존 `Plan Tree`를 체크박스 목록으로 쓰면 `Checklist`와 역할이 겹칩니다. 예를 들어 `Plan Tree`와 `Checklist`가 모두 `[ ]`, `[x]`, `(pending)`, `(done)`을 가지면 같은 상태를 두 곳에서 수정해야 하며, 둘 중 하나가 쉽게 낡습니다.

반면 `Plan Tree`를 체크박스 없는 텍스트 트리로 두면 책임이 분명해집니다.

- `Plan Tree`: 구조와 현재 작업 위치를 보여주는 읽기용 지도
- `Checklist`: 실제 상태 추적의 source of truth

tree glyph를 사용하면 대형 계획의 묶음과 하위 작업을 더 쉽게 읽을 수 있습니다.

예시:

```text
P1. 착수 처리
├─ P1.1. 계획서를 `doing`으로 이동
└─ P1.2. 상태와 README 목록 갱신

P2. README 갱신 [now]
├─ P2.1. Workflow 섹션 추가
├─ P2.2. Mermaid 다이어그램 추가
└─ P2.3. 실행 권한 계층 요약

P3. AGENTS 갱신
├─ P3.1. 단계별 참조 규칙 추가
├─ P3.2. 보고서 참조 제한 추가
└─ P3.3. 세션 업데이트 조건 강화
```

`[now]`는 읽기용 힌트입니다. 전체 항목에 `[done]`, `[pending]`을 붙이면 `Checklist`와 중복되므로 권장하지 않습니다.

논의 문서의 경우 실행 추적보다 판단 준비 상태가 중요합니다. 따라서 계획 문서처럼 실행 체크리스트를 강제하지 않는 편이 더 적합합니다.

## Options (대안)

옵션 A: 기존 체크박스형 `Plan Tree`를 유지합니다.

- 장점: 현재 형식과 호환됩니다.
- 장점: Markdown 체크박스만으로 진행 상태를 볼 수 있습니다.
- 단점: `Checklist`와 역할이 겹칩니다.
- 단점: 대형 계획에서 계층 구조가 잘 보이지 않습니다.

옵션 B: `Plan Tree`를 tree glyph 기반 텍스트 트리로 바꾸고 체크박스를 제거합니다.

- 장점: 구조가 명확하게 보입니다.
- 장점: `Checklist`와 책임이 분리됩니다.
- 장점: `[now]`로 현재 위치만 가볍게 표시할 수 있습니다.
- 단점: 체크박스 렌더링으로 바로 완료 상태를 볼 수는 없습니다.
- 단점: tree glyph를 직접 관리해야 합니다.

옵션 C: `Plan Tree`는 표로 작성합니다.

- 장점: ID, 작업, 상태를 열로 분리할 수 있습니다.
- 단점: 수정이 번거롭습니다.
- 단점: LLM이나 수동 편집자가 표 정렬을 깨뜨릴 수 있습니다.
- 단점: `Checklist`와 상태 중복 문제가 남을 수 있습니다.

옵션 D: `Plan Tree`에는 `P1/P1.1` flat list만 사용합니다.

- 장점: ASCII 중심이라 깨질 가능성이 낮습니다.
- 장점: 검색과 편집이 쉽습니다.
- 단점: tree glyph보다 시각적 계층이 약합니다.

## Trade-offs (트레이드오프)

옵션 B는 사람이 읽는 가독성과 역할 분리 측면에서 가장 좋습니다. 다만 상태를 트리와 체크리스트 양쪽에 기록하지 않도록 규칙을 명확히 해야 합니다.

`[now]`는 유용하지만 남용하면 또 다른 상태 추적 체계가 됩니다. 따라서 `[now]`는 한 번에 하나만 유지하고, 완료/대기/중단 상태는 `Checklist`에만 기록하는 편이 안전합니다.

계획 문서에는 최소 필수 체크리스트 항목이 있으면 완료 기준이 흔들리지 않습니다. 반면 논의 문서는 실행 문서가 아니므로 체크리스트를 추가하지 않는 편이 적절합니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안은 옵션 B입니다.

`Plan Tree` 규칙:

- `Plan Tree`는 작업 구조와 현재 위치를 보여주는 읽기용 지도입니다.
- `Plan Tree`에는 체크박스를 넣지 않습니다.
- `Plan Tree`는 fenced `text` 코드 블록에 작성합니다.
- `Plan Tree`는 `P1`, `P1.1`, `P2`, `P2.1` 같은 ID를 사용합니다.
- `Plan Tree`는 `├─`, `└─`, `│` 같은 tree glyph를 사용할 수 있습니다.
- 현재 작업 중인 항목은 선택적으로 `[now]`를 붙입니다.
- `[now]`는 한 번에 하나만 유지합니다.
- 완료, 대기, 중단 상태는 `Checklist`에서 관리합니다.

`Checklist` 규칙:

- `Checklist`는 실제 상태 추적의 source of truth입니다.
- `Checklist`는 `CL-001` 형식의 ID를 사용합니다.
- 각 항목은 체크박스와 상태 값을 함께 둡니다.
- 허용 상태 값은 기존처럼 `pending`, `now doing`, `done`, `aborted`를 유지합니다.
- `Plan Tree`의 `[now]`와 `Checklist`의 `(now doing)`은 가능하면 같은 작업을 가리키게 합니다.

계획 문서 최소 체크리스트 예시:

```md
## Checklist (전체 체크리스트)

- [ ] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (pending)
- [ ] CL-002: 계획 범위의 변경을 수행 (pending)
- [ ] CL-003: 관련 문서와 상태 목록을 검증 (pending)
- [ ] CL-004: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (pending)
```

## Decision Candidate (결정 후보)

아직 확정 전이지만 현재 결정 후보는 다음과 같습니다.

- 계획 문서의 `Plan Tree`는 체크박스 없는 tree glyph 기반 텍스트 트리로 작성합니다.
- `Plan Tree`는 구조와 현재 위치를 보여주는 읽기용 지도입니다.
- `Checklist`는 실제 상태 추적의 source of truth입니다.
- `Plan Tree`에는 `[now]`만 선택적으로 표시하고, 한 번에 하나만 유지합니다.
- 완료/대기/중단 상태는 `Checklist`에서 관리합니다.
- 계획 문서 README에는 최소 필수 체크리스트 예시를 강화합니다.
- 논의 문서에는 별도 체크리스트를 추가하지 않습니다.
- 기존 완료 문서 전체를 일괄 수정하지 않고, 새 문서 작성 규칙과 예시만 개선합니다.
- `Plan Tree`의 `[now]` 표기는 영어 `now`만 허용합니다.
- `Plan Tree`의 `P1/P1.1` ID와 `Checklist`의 `CL-001` ID 매핑은 `Checklist` 쪽에 `P:` 필드로 둡니다.
- 계획 문서 최소 체크리스트 항목은 필수로 둡니다.
- 이 규칙은 `docs/plans/README.md`에 반영하고, `AGENTS.md`에는 추가하지 않습니다.

## Questions (질문)

- `Plan Tree`의 `[now]` 표기는 영어 그대로 유지할까요, 아니면 한국어 문서에서는 `[현재]`도 허용할까요?
  답변: `now`만 허용합니다.
- `Plan Tree`에서 `P1/P1.1` ID와 `Checklist`의 `CL-001` ID를 연결하는 별도 매핑을 둘 필요가 있을까요?
  답변: 한쪽에는 매핑 정보를 둡니다. `Plan Tree`를 깨끗하게 유지하기 위해 `Checklist` 항목에 `P:` 필드로 둡니다.
- 계획 문서 최소 체크리스트 4개 항목을 필수로 둘까요, 아니면 강한 권장 예시로 둘까요?
  답변: 필수로 둡니다.
- `Decision Readiness Checklist`를 논의 문서의 권장 섹션으로 추가할까요, 아니면 README 예시로만 둘까요?
  답변: 논의 문서 성격상 별로 필요하지 않으므로 추가하지 않습니다.
- 기존 `docs/plans/README.md`의 예시만 바꾸면 충분할까요, `AGENTS.md`에도 핵심 규칙을 반영해야 할까요?
  답변: `AGENTS.md`에는 추가하지 않습니다.

## Open Issues (열린 쟁점)

- tree glyph 사용은 가독성이 좋지만, 작성자가 실수로 트리 문자를 깨뜨릴 수 있습니다.
- 작은 계획에서도 같은 형식을 강제하면 문서 작성 비용이 커질 수 있습니다.

## Resolution (정리 결과)

사용자 승인에 따라 다음 결론으로 확정합니다.

- `Plan Tree`는 체크박스 없는 tree glyph 기반 `text` 코드 블록으로 작성합니다.
- `Plan Tree`는 구조와 현재 위치를 보여주는 읽기용 지도입니다.
- 실제 상태 추적의 source of truth는 `Checklist`입니다.
- `Plan Tree`에는 `[now]`만 선택적으로 표시하고, 한 번에 하나만 유지합니다.
- `[now]` 표기는 영어 `now`만 허용합니다.
- `Checklist` 항목에는 관련 `Plan Tree` ID를 `P:` 필드로 매핑합니다.
- 계획 문서의 최소 체크리스트 항목은 필수로 둡니다.
- 논의 문서에는 별도 decision readiness 체크리스트를 추가하지 않습니다.
- 이번 규칙은 `docs/plans/README.md`에 반영하고, `AGENTS.md`에는 추가하지 않습니다.
- 기존 완료 문서 전체를 일괄 수정하지 않고, 새 문서 작성 규칙과 예시만 개선합니다.

이 결론은 다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_14-59-51_plan-tree-checklist-readability.md`

## Absorption Target (흡수 대상)

다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_14-59-51_plan-tree-checklist-readability.md`

계획 실행 후 다음 문서에 반영합니다.

- `docs/plans/README.md`

## References (근거 및 영향 문서)

근거:

- 사용자 요청: 계획서 트리 구조 가독성 개선 필요
- 사용자 요청: 논의/계획 문서 체크리스트의 필수 목록 지정 또는 예시 강화 필요
- 사용자 선호: `Plan Tree`에는 체크리스트를 넣지 않고, 현재 작업 중인 항목 정도만 표시
- `docs/plans/README.md`
- `.project-context/discussions/README.md`

영향:

- `docs/plans/README.md`
- 향후 작성되는 `docs/plans/{scheduled|doing|archived}/` 문서
