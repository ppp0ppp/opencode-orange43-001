# Discussion: 대형 작업의 논의와 계획 분할 관리

## Status (상태)

closed

## Summary (요약)

대형 구현, 개편, 논의, 계획은 하나의 문서만으로 관리하면 범위와 진행 상태가 커져 추적성이 떨어질 수 있습니다. 이 논의는 상위 논의/계획과 하위 논의/계획을 어떻게 나누고, 어떤 깊이까지 허용하며, opencode Todo 같은 실행 단위와 계획서 체크리스트를 어떻게 구분할지 정합니다.

최종 결론은 일반 계획/논의는 기존처럼 상태 디렉토리 바로 아래 `.md` 파일로 두고, 대형 계획/논의는 상태 디렉토리 바로 아래 디렉토리로 두는 방식입니다. 대형 디렉토리 내부에는 `main-plan.md` 또는 `main-discussion.md`와 하위 상태 디렉토리를 두며, 하위 문서는 한 단계만 허용합니다.

## Background (배경)

현재 공식 계획 문서는 `docs/plans/{scheduled|doing|archived}/`에 두고, 논의 문서는 `.project-context/discussions/{draft|open|closed}/`에 둡니다. 각 문서는 최초 생성 시각 기준 `YYYY-MM-DD_HH-MM-SS_detail-title.md` 형식을 사용하며, 상태 이동 시 파일명은 유지합니다.

대형 작업에서는 하나의 계획서에 모든 체크리스트를 넣으면 문서가 과도하게 커질 수 있습니다. 반대로 모든 세부 작업을 별도 계획서로 만들면 상위 목표와 현재 진행 상태를 한눈에 파악하기 어려워질 수 있습니다.

사용자는 다음 후보를 제시했습니다.

- 디렉토리명으로 `YYYY-MM-DD_HH-MM-SS_detail-title`을 사용하고 내부에 하위 계획을 관리합니다.
- 기존 계획/논의 문서 구조는 유지하되 하위 계획/논의용 하위 디렉토리를 추가합니다.
- `docs/plans/doing/sub/YYYY-MM-DD_HH-MM-SS_detail-title.md/YYYY-MM-DD_HH-MM-SS_sub-plan-detail-title.md`처럼 표현하되, 이 이상 깊어지는 것은 허용하지 않습니다.
- 실제 도입 여부는 논의를 거쳐 사용자와 함께 판단합니다.

## Context (맥락)

관련 현재 규칙:

- 공식 계획 문서는 `docs/plans/{scheduled|doing|archived}/`에 둡니다.
- 논의 문서는 `.project-context/discussions/{draft|open|closed}/`에 둡니다.
- 계획 문서와 논의 문서는 상태 디렉토리와 본문 `Status (상태)`가 일치해야 합니다.
- 문서 경로는 프로젝트 루트 기준 경로로 적습니다.
- README 문서 목록도 프로젝트 루트 기준 경로를 사용합니다.

opencode Todo의 성격:

- Todo는 현재 세션 또는 현재 작업 턴의 최소 실행 단위 관리 도구입니다.
- 계획서의 `Checklist (전체 체크리스트)`는 문서화된 계획 추적 단위입니다.
- 두 단위는 1:1로 대응하지 않을 수 있습니다.

## Scope (범위)

포함:

- 대형 논의/계획을 하위 문서로 분할하는 구조 선택
- 하위 논의/계획 문서의 위치, 이름, 깊이 제한
- 상위 문서와 하위 문서의 참조 방식
- opencode Todo와 계획서 체크리스트의 책임 구분
- 관련 규칙을 어느 공식 문서에 흡수할지 결정

제외:

- 자동 문서 생성기 또는 링크 검증 도구 도입
- 기존 완료 문서 전체의 대규모 재작성
- 제품 코드 구현 방식 논의
- opencode 자체 Todo 기능의 동작 변경

## Constraints (제약)

- 경로 표기는 프로젝트 루트 기준 경로를 유지합니다.
- 상태 디렉토리와 본문 상태가 일치해야 합니다.
- 하위 구조는 사람이 수동으로 관리할 수 있을 만큼 단순해야 합니다.
- 하위 계획/논의가 무한히 깊어지지 않도록 제한해야 합니다.
- 논의 문서와 계획 문서의 목적 차이를 유지해야 합니다.
- opencode Todo는 계획서 체크리스트의 대체물이 아니라 실행 보조 도구로 정의해야 합니다.

## Analysis (분석)

대형 작업 관리에서 필요한 것은 세 가지입니다.

- 상위 목표와 전체 진행률을 보는 지도
- 실제 실행 가능한 하위 단위의 독립 추적
- 세션 단위 실행 상태를 잃지 않는 짧은 Todo 관리

상위 계획서 하나에 모든 세부 항목을 넣으면 상위 지도는 유지되지만 문서가 커집니다. 하위 문서를 분리하면 개별 추적은 좋아지지만 경로 규칙, 상태 이동, 상위 문서의 링크 관리가 복잡해집니다.

논의와 계획은 서로 다른 단계입니다. 논의는 결정 전 대안과 판단을 다루고, 계획은 실행 범위와 체크리스트를 다룹니다. 따라서 하위 문서 구조를 도입하더라도 논의 하위 문서와 계획 하위 문서의 위치와 상태 규칙은 각각의 기존 상태 디렉토리를 따라야 합니다.

Todo와 계획 체크리스트는 시간 범위가 다릅니다. Todo는 한 번의 작업 세션에서 실행할 최소 작업 단위이고, 계획 체크리스트는 문서로 보존되는 계획 추적 단위입니다. 하나의 Todo 목록이 하나의 계획서 전체를 처리할 수도 있고, 여러 체크리스트를 처리할 수도 있으며, 단일 체크리스트를 여러 Todo 목록으로 나누어 처리할 수도 있습니다. 사용자의 간단한 지시나 작은 작업은 논의/계획 없이 Todo만으로 처리하거나 Todo 없이 바로 처리할 수도 있습니다.

## Options (대안)

옵션 A: 상위 디렉토리 방식

- 예: `docs/plans/doing/2026-06-13_13-17-01_large-work/plan.md`
- 하위 계획은 같은 디렉토리 안에 둡니다.
- 장점: 관련 파일이 한 디렉토리에 모여 탐색하기 쉽습니다.
- 단점: 현재 파일명 규칙과 상태 이동 규칙을 바꿔야 합니다.
- 단점: README 문서 목록과 기존 경로 표준이 복잡해집니다.

옵션 B: 대형 디렉토리와 내부 상태 디렉토리 방식

- 예: `docs/plans/doing/2026-06-13_13-17-01_large-work/main-plan.md`
- 예: `docs/plans/doing/2026-06-13_13-17-01_large-work/doing/2026-06-13_13-20-00_sub-plan.md`
- 논의도 같은 패턴으로 `.project-context/discussions/open/...` 아래에 `main-discussion.md`와 내부 상태 디렉토리를 사용합니다.
- 일반 문서는 기존처럼 상태 디렉토리 바로 아래 `.md` 파일로 둡니다.
- 장점: 기존 문서 파일 규칙을 유지하면서 하위 문서를 분리할 수 있습니다.
- 장점: 대형 문서라는 의미가 경로에 명확히 드러납니다.
- 장점: 대형 문서의 상태와 하위 문서의 상태를 분리해 관리할 수 있습니다.
- 단점: 대형 디렉토리의 main 문서와 하위 상태 디렉토리 규칙을 명확히 해야 합니다.

옵션 C: 하위 문서 없이 상위 문서의 섹션만 사용

- 예: 상위 계획서의 `Plan Tree`, `Checklist`, `Progress Notes`를 더 엄격하게 운용합니다.
- 장점: 구조 변경이 없습니다.
- 장점: 상태 이동과 문서 목록 관리가 단순합니다.
- 단점: 대형 작업에서 문서가 지나치게 커질 수 있습니다.
- 단점: 병렬 하위 작업의 독립적인 논의/검증 기록이 어려울 수 있습니다.

옵션 D: 관련 계획/논의를 병렬 문서로 두고 상호 참조만 사용

- 예: 여러 계획서를 `docs/plans/doing/`에 나란히 두고 상위 계획의 `Dependencies`와 `References`에 연결합니다.
- 장점: 현재 상태 디렉토리 구조와 완전히 호환됩니다.
- 단점: 어떤 문서가 상위이고 하위인지 경로만으로는 알기 어렵습니다.
- 단점: README 목록과 문서 제목만으로 계층 관계를 파악하기 어렵습니다.

## Trade-offs (트레이드오프)

옵션 A는 파일 묶음 관점에서는 자연스럽지만 현재 `YYYY-MM-DD_HH-MM-SS_detail-title.md` 파일 규칙을 디렉토리 규칙으로 바꿔야 합니다. 기존 문서 운영 원칙을 크게 바꾸므로 비용이 큽니다.

옵션 B는 사용자가 최종 선호한 방향입니다. 대형 문서라는 사실이 경로에서 드러나고, 하위 문서 상태를 내부 상태 디렉토리로 독립 추적할 수 있습니다. 다만 더 깊은 중첩을 금지하고 README 목록 범위를 제한해야 관리 비용이 커지지 않습니다.

옵션 C는 가장 단순하지만 대형 작업의 핵심 문제인 문서 비대화를 해결하지 못합니다.

옵션 D는 현재 구조에 가장 안전하지만, 계층이 암묵적이어서 장기 추적성이 떨어질 수 있습니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안은 옵션 B입니다.

확정 규칙:

- 일반 논의/계획은 기존 상태 디렉토리 바로 아래 `.md` 파일로 둡니다.
- 대형 논의/계획은 기존 상태 디렉토리 바로 아래 디렉토리로 둡니다.
- 대형 계획 디렉토리는 `main-plan.md`를 포함합니다.
- 대형 논의 디렉토리는 `main-discussion.md`를 포함합니다.
- 대형 계획 디렉토리의 외부 상태는 `main-plan.md`의 상태를 따릅니다.
- 대형 논의 디렉토리의 외부 상태는 `main-discussion.md`의 상태를 따릅니다.
- 대형 디렉토리 내부의 하위 문서는 내부 상태 디렉토리의 상태를 따릅니다.
- plans 내부 상태 디렉토리는 `scheduled`, `doing`, `archived`를 사용합니다.
- discussions 내부 상태 디렉토리는 `draft`, `open`, `closed`를 사용합니다.
- 하위 문서는 한 단계만 허용하고, 하위 문서 아래에 다시 하위 디렉토리를 만들지 않습니다.
- 하위 문서도 `YYYY-MM-DD_HH-MM-SS_detail-title.md` 형식을 사용합니다.
- README 문서 목록은 상태 디렉토리 바로 아래 일반 문서와 대형 디렉토리까지만 나열합니다.
- 하위 문서 목록과 진행 관리는 `main-plan.md` 또는 `main-discussion.md`에서 담당합니다.

예시:

```text
docs/plans/doing/2026-06-13_13-17-01_large-work/
docs/plans/doing/2026-06-13_13-17-01_large-work/main-plan.md
docs/plans/doing/2026-06-13_13-17-01_large-work/scheduled/2026-06-13_13-20-00_sub-plan-a.md
docs/plans/doing/2026-06-13_13-17-01_large-work/doing/2026-06-13_13-25-00_sub-plan-b.md
docs/plans/doing/2026-06-13_13-17-01_large-work/archived/2026-06-13_13-30-00_sub-plan-c.md
.project-context/discussions/open/2026-06-13_13-17-01_large-work/
.project-context/discussions/open/2026-06-13_13-17-01_large-work/main-discussion.md
.project-context/discussions/open/2026-06-13_13-17-01_large-work/draft/2026-06-13_13-20-00_sub-topic-a.md
.project-context/discussions/open/2026-06-13_13-17-01_large-work/open/2026-06-13_13-25-00_sub-topic-b.md
.project-context/discussions/open/2026-06-13_13-17-01_large-work/closed/2026-06-13_13-30-00_sub-topic-c.md
```

허용하지 않는 예시:

```text
docs/plans/doing/parent/doing/child/doing/grandchild.md
.project-context/discussions/open/parent/open/child/open/grandchild.md
```

상위 문서에는 다음을 명시합니다.

- `Dependencies (의존성)` 또는 `References (근거 및 영향 문서)`에 하위 문서 목록
- `Plan Tree (계획 트리)` 또는 `Analysis (분석)`에 하위 문서가 담당하는 범위
- 하위 문서가 완료되거나 중단될 때 상위 문서의 체크리스트 또는 진행 메모 갱신

하위 문서에는 다음을 명시합니다.

- 상위 문서 경로
- 자신이 담당하는 범위
- 상위 문서와 중복하지 않는 체크리스트 또는 논의 범위
- 완료 시 상위 문서에 반영해야 하는 결과

Todo 관련 규칙은 `AGENTS.md`, `docs/plans/README.md`, `.project-context/discussions/README.md` 중 적어도 `AGENTS.md`와 `docs/plans/README.md`에 흡수하는 것을 권장합니다.

## Decision Candidate (결정 후보)

확정된 결정 후보이며, 실행 계획서로 흡수합니다.

- 일반 계획/논의는 기존처럼 `.md` 파일로 관리합니다.
- 대형 계획/논의는 디렉토리로 관리합니다.
- 대형 계획은 `main-plan.md`, 대형 논의는 `main-discussion.md`를 기준 문서로 둡니다.
- 대형 디렉토리의 외부 상태는 main 문서의 상태를 따릅니다.
- 하위 문서의 상태는 대형 디렉토리 내부 상태 디렉토리를 따릅니다.
- 하위 문서는 한 단계만 허용합니다.
- README 문서 목록은 상태 디렉토리 바로 아래 일반 문서와 대형 디렉토리까지만 나열합니다.
- Todo는 세션 실행 단위, 계획 체크리스트는 문서 추적 단위로 명시합니다.

## Questions (질문)

- 하위 문서 디렉토리는 `sub/상위문서명/하위문서.md` 형태가 적절합니까?
  답변: 아니요. 대형 계획/논의 자체를 디렉토리로 두고 내부에 `main-plan.md` 또는 `main-discussion.md`와 상태 디렉토리를 둡니다.
- 하위 계획/논의는 상위 문서와 항상 같은 상태 디렉토리로 함께 이동해야 합니까, 아니면 독립 상태를 허용해야 합니까?
  답변: 대형 디렉토리의 외부 상태는 main 문서의 상태를 따르고, 하위 문서의 상태는 대형 디렉토리 내부 상태 디렉토리를 따릅니다.
- `sub/` 구조는 plans와 discussions 양쪽에 동일하게 적용합니까?
  답변: `sub/` 구조는 쓰지 않습니다. 대형 디렉토리 구조를 plans와 discussions 양쪽에 동일하게 적용하되, 상태명은 각 문서 체계의 기존 상태명을 따릅니다.
- 하위 문서를 README 문서 목록에 모두 나열해야 합니까, 아니면 상위 문서 아래에만 기록합니까?
  답변: README에는 상태 디렉토리 바로 아래 일반 문서와 대형 디렉토리까지만 나열합니다. 하위 문서 목록은 main 문서에서 관리합니다.
- Todo와 계획 체크리스트의 관계 설명은 `AGENTS.md`와 `docs/plans/README.md`에 둘까요, 아니면 `.project-context/discussions/README.md`에도 둘까요?
  답변: `AGENTS.md`와 `docs/plans/README.md`에 둡니다.
- 간단한 사용자 지시나 작은 작업은 논의/계획 없이 진행할 수 있다는 규칙을 `AGENTS.md`에 명시하면 충분합니까?
  답변: 네.

## Open Issues (열린 쟁점)

현재 없음

## Resolution (정리 결과)

대형 계획/논의는 상태 디렉토리 바로 아래 디렉토리로 관리합니다. 대형 계획은 `main-plan.md`, 대형 논의는 `main-discussion.md`를 포함하며, 내부에는 하위 문서 상태를 나타내는 상태 디렉토리를 둡니다.

plans의 상태명은 `scheduled`, `doing`, `archived`를 유지하고, discussions의 상태명은 `draft`, `open`, `closed`를 유지합니다. README 목록은 상태 디렉토리 바로 아래 일반 문서와 대형 디렉토리까지만 나열하며, 하위 문서 목록과 진행 관리는 main 문서가 담당합니다.

Todo는 세션 실행 단위이고 계획서 체크리스트는 문서 추적 단위입니다. 간단한 사용자 지시나 작은 작업은 논의/계획 없이 진행할 수 있습니다.

## Absorption Target (흡수 대상)

논의 결론은 다음 계획서로 흡수합니다.

- `docs/plans/archived/2026-06-13_13-31-48_large-work-breakdown-tracking.md`

계획 실행 후 다음 문서에 반영합니다.

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`

## References (근거 및 영향 문서)

근거:

- 사용자 요청: 대형 구현/개편/논의/계획의 분할 관리 방식 논의
- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`

영향:

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`
- 향후 작성되는 `docs/plans/{scheduled|doing|archived}/` 문서
- 향후 작성되는 `.project-context/discussions/{draft|open|closed}/` 문서
