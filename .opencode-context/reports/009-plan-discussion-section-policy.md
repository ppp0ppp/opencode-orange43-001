# Plan And Discussion Section Policy Review

작성일: 2026-06-13

## 결론

`docs/plans`와 `.opencode-context/discussions`는 서로 다른 목적을 가지므로 섹션 세트도 다르게 두는 편이 좋습니다.

권장 방향은 다음과 같습니다.

- 계획 문서(`plans`)는 실행과 추적 중심으로 구성합니다.
- 논의 문서(`discussions`)는 판단 형성과 질문/답변 중심으로 구성합니다.
- 두 문서 모두 필수 섹션 외에 권장 섹션을 README에 명시하되, 모든 문서에 강제하지는 않습니다.
- README에는 영문 타이틀과 한글명칭을 함께 쓰고, 각 섹션에 넣을 내용 설명과 짧은 예시를 둡니다.
- 루트 `docs-context-restructure-discussion.md`는 승인 후 `.opencode-context/discussions/closed/`로 이동합니다.
- `AGENTS.md`의 중복 `Graphify Policy` 정리는 이번 정합성 수정 범위에 포함합니다.
- `docs/plans/scheduled`는 미승인 계획과 승인됐지만 아직 착수하지 않은 계획을 모두 포함합니다.

## 반영된 사용자 판단

이번 보고서에 반영한 사용자 판단은 다음과 같습니다.

- 루트에 생성된 `docs-context-restructure-discussion.md`는 승인 후 `.opencode-context/discussions/closed/`로 이동합니다.
- `AGENTS.md`의 중복 `Graphify Policy` 섹션 정리는 이번 정합성 수정에 포함합니다.
- `docs/plans/scheduled`는 미승인 계획과 승인됐지만 아직 착수하지 않은 계획을 모두 포함합니다.
- 계획 문서와 논의 문서는 필수 섹션 외의 권장 섹션을 정하고, 각 README에 섹션 설명 또는 예시를 둡니다.

## 문서 상태 의미 보정

`docs/plans/scheduled`:

- 아직 승인되지 않은 계획서를 둡니다.
- 승인됐지만 아직 착수하지 않은 계획서도 둡니다.
- 실행으로 전환되면 `docs/plans/open`으로 이동합니다.

`docs/plans/open`:

- 실제 실행 중인 계획서를 둡니다.
- 여러 계획이 동시에 열릴 수 있으나, 서로 영향을 주면 `Dependencies (의존성)` 또는 `References (근거 및 영향 문서)`에 명시합니다.

`docs/plans/closed`:

- 모든 항목이 `done` 또는 명시적으로 `aborted` 처리된 계획서를 둡니다.
- 완료 후 회고나 결과 요약을 남기는 것이 좋습니다.

`.opencode-context/discussions/draft`:

- 초안, 미정의 주제, 에이전트가 먼저 제안한 문서를 둡니다.
- 사용자와 본격적으로 질문/답변을 시작하기 전 상태입니다.

`.opencode-context/discussions/open`:

- 사용자와 에이전트가 질문/답변, 수정, 판단을 진행 중인 문서를 둡니다.
- 결론이 아직 공식 문서에 흡수되지 않은 상태입니다.

`.opencode-context/discussions/closed`:

- 논의가 끝났고 필요한 내용이 `docs/contracts`, `docs/architectures`, `docs/plans`, README 등으로 흡수된 문서를 둡니다.
- 닫힌 논의 문서는 최종 규칙의 원본이 아니라 히스토리와 근거 역할을 합니다.

## 계획 문서 섹션 세트 제안

계획 문서 README에는 다음 섹션 세트를 제안합니다.

필수 섹션:

- `Status (상태)`
- `Scope (작업 범위)`
- `Plan Ground (계획 기반 체크리스트)`
- `Plan Tree (계획 트리)`
- `Checklist (전체 체크리스트)`
- `References (근거 및 영향 문서)`

권장 섹션:

- `Summary (요약)`
- `Goal (목표)`
- `Non-Goals (제외 목표)`
- `Assumptions (가정)`
- `Dependencies (의존성)`
- `Risks (리스크)`
- `Verification (검증)`
- `Rollback Or Abort Plan (롤백 또는 중단 계획)`
- `Progress Notes (진행 메모)`
- `Result (결과)`

## 계획 문서 필수 섹션 설명안

`Status (상태)`:

- 현재 계획서의 상태를 적습니다.
- 허용 값은 `scheduled`, `open`, `closed`입니다.
- 파일이 위치한 상태 디렉토리와 본문 상태는 같아야 합니다.

예시:

```md
## Status (상태)

scheduled
```

`Scope (작업 범위)`:

- 본 계획이 포함하는 작업과 제외하는 작업을 적습니다.
- 구현, 문서화, 검증, 마이그레이션 등 범위를 분리해 적으면 좋습니다.

예시:

```md
## Scope (작업 범위)

포함:

- `docs/plans` 구조 생성
- 관련 README 갱신

제외:

- 문서 자동 생성기 도입
- 기존 보고서 내용 재작성
```

`Plan Ground (계획 기반 체크리스트)`:

- 계획 전체를 일반 분류별 체크리스트로 정리합니다.
- 작업의 큰 묶음을 한눈에 보기 위한 섹션입니다.
- 세부 순서보다 범주가 중요합니다.

예시:

```md
## Plan Ground (계획 기반 체크리스트)

- [ ] 구조 변경
- [ ] README 갱신
- [ ] 지침 정합성 수정
- [ ] 검증
```

`Plan Tree (계획 트리)`:

- 계획을 단계적으로 표현합니다.
- 선후관계, 하위 작업, 블로커를 드러내는 데 사용합니다.
- Markdown에서는 들여쓰기 대신 단계 번호나 경로 표기를 사용해도 됩니다.

예시:

```md
## Plan Tree (계획 트리)

- [ ] 1. 문서 구조 생성
- [ ] 1.1. `docs/contracts` 이동
- [ ] 1.2. `docs/architectures` 추가
- [ ] 1.3. `docs/plans` 상태 디렉토리 추가
- [ ] 2. 지침 갱신
- [ ] 2.1. `AGENTS.md` 수정
- [ ] 2.2. README 정합성 수정
```

`Checklist (전체 체크리스트)`:

- 모든 체크리스트 항목을 `CL-001` 형식으로 모읍니다.
- 각 항목에는 체크박스와 상태 값을 함께 둡니다.
- 허용 상태 값은 `done`, `now doing`, `pending`, `aborted`입니다.

예시:

```md
## Checklist (전체 체크리스트)

- [ ] CL-001: `docs/contracts` 이동 (pending)
- [ ] CL-002: `docs/plans/README.md` 작성 (now doing)
- [x] CL-003: 기존 구조 조사 (done)
- [ ] CL-004: 자동 리스팅 도입 (aborted)
```

`References (근거 및 영향 문서)`:

- 계획의 근거가 되는 문서와 영향을 받는 문서를 적습니다.
- 관련 논의, 보고서, 계약, 아키텍처, README, 코드 경로를 포함할 수 있습니다.

예시:

```md
## References (근거 및 영향 문서)

근거:

- `.opencode-context/reports/008-docs-context-structure-consistency.md`

영향:

- `AGENTS.md`
- `docs/README.md`
- `.opencode-context/README.md`
```

## 계획 문서 권장 섹션 설명안

`Summary (요약)`:

- 계획의 목적과 핵심 작업을 2~5문장으로 요약합니다.
- 긴 계획서에서 독자가 먼저 읽는 부분입니다.

`Goal (목표)`:

- 완료되면 무엇이 달라져야 하는지 적습니다.
- 성공 기준이 명확하면 함께 적습니다.

`Non-Goals (제외 목표)`:

- 이번 계획에서 하지 않을 일을 적습니다.
- 범위 확장을 막기 위한 섹션입니다.

`Assumptions (가정)`:

- 계획이 성립하기 위해 참이라고 보는 조건을 적습니다.
- 가정이 깨지면 계획 변경이 필요할 수 있습니다.

`Dependencies (의존성)`:

- 다른 계획, 논의, 문서, 코드 변경과의 의존성을 적습니다.
- 동시에 진행 중인 계획과 커플링이 있으면 반드시 적습니다.

`Risks (리스크)`:

- 기술적, 운영적, 문서 정합성, 일정 리스크를 적습니다.
- 리스크별 완화책을 같이 적으면 좋습니다.

`Verification (검증)`:

- 계획 완료를 어떻게 확인할지 적습니다.
- 테스트, 빌드, 문서 링크 확인, grep 확인 등을 포함할 수 있습니다.

`Rollback Or Abort Plan (롤백 또는 중단 계획)`:

- 계획을 중단하거나 되돌려야 할 조건과 처리 방식을 적습니다.
- 문서 작업이라도 삭제, 이동, 상태 복구 기준을 적을 수 있습니다.

`Progress Notes (진행 메모)`:

- 진행 중 발견한 중요한 사실과 상태 변경을 적습니다.
- 세션 체크포인트보다 해당 계획에 종속적인 메모만 둡니다.

`Result (결과)`:

- `closed` 상태로 이동할 때 최종 결과를 적습니다.
- 완료된 변경, 생략된 항목, 후속 계획을 포함할 수 있습니다.

## 논의 문서 섹션 세트 제안

논의 문서 README에는 다음 섹션 세트를 제안합니다.

필수 섹션:

- `Status (상태)`
- `Scope (범위)`
- `Analysis (분석)`
- `Recommended Strategy / Plan / Options (추천 전략/계획/옵션)`
- `Questions (질문)`
- `References (근거 및 영향 문서)`

권장 섹션:

- `Summary (요약)`
- `Background (배경)`
- `Context (맥락)`
- `Constraints (제약)`
- `Options (대안)`
- `Trade-offs (트레이드오프)`
- `Decision Candidate (결정 후보)`
- `Open Issues (열린 쟁점)`
- `Resolution (정리 결과)`
- `Absorption Target (흡수 대상)`

## 논의 문서 필수 섹션 설명안

`Status (상태)`:

- 현재 논의 문서의 상태를 적습니다.
- 허용 값은 `draft`, `open`, `closed`입니다.
- 파일이 위치한 상태 디렉토리와 본문 상태는 같아야 합니다.

예시:

```md
## Status (상태)

open
```

`Scope (범위)`:

- 본 논의가 다루는 주제와 다루지 않는 주제를 적습니다.
- 질문을 넓히기 전에 논의 경계를 확인하는 역할입니다.

예시:

```md
## Scope (범위)

포함:

- 문서 구조 개편 방향
- 계획/논의 문서 상태 정의

제외:

- CI 자동화
- 제품 기능 설계
```

`Analysis (분석)`:

- 현재 상태, 문제, 관찰, 리스크를 적습니다.
- 사실과 추정을 구분하면 좋습니다.

예시:

```md
## Analysis (분석)

- 현재 계약 문서는 `.opencode-context/contracts`에 있습니다.
- 새 구조에서는 공식 계약 문서가 `docs/contracts`로 이동해야 합니다.
- `AGENTS.md`가 갱신되지 않으면 에이전트 행동 지침과 문서 구조가 충돌합니다.
```

`Recommended Strategy / Plan / Options (추천 전략/계획/옵션)`:

- 추천 전략, 실행 계획, 또는 선택 가능한 대안을 적습니다.
- 하나의 추천안이 있으면 먼저 쓰고, 대안은 뒤에 둡니다.

예시:

```md
## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안:

- `docs/`를 공식 문서 위치로 둡니다.
- `.opencode-context/`는 논의, 보고서, 세션, 입력 자료 중심으로 축소합니다.

대안:

- `.opencode-context/decisions`를 유지하되 공식 문서와 상호 참조합니다.
```

`Questions (질문)`:

- 사용자 판단이 필요한 질문을 적습니다.
- 답변이 들어오면 같은 섹션에 답변을 붙이거나, `Resolution (정리 결과)`에 반영합니다.

예시:

```md
## Questions (질문)

- `scheduled`는 미승인만 의미합니까?
- `AGENTS.md` 정합성 수정도 이번 범위에 포함합니까?
```

`References (근거 및 영향 문서)`:

- 논의의 근거 문서와 영향을 받을 문서를 적습니다.
- 논의가 닫힐 때 흡수된 공식 문서도 함께 적습니다.

예시:

```md
## References (근거 및 영향 문서)

근거:

- `.opencode-context/reports/008-docs-context-structure-consistency.md`

영향:

- `docs/plans/README.md`
- `.opencode-context/discussions/README.md`
```

## 논의 문서 권장 섹션 설명안

`Summary (요약)`:

- 논의 주제와 현재 결론을 짧게 적습니다.
- `open` 상태에서는 현재 선호안을 적고, `closed` 상태에서는 최종 흡수 결과를 적습니다.

`Background (배경)`:

- 왜 이 논의가 시작됐는지 적습니다.
- 사용자 요청, 이전 보고서, 문제 상황을 포함할 수 있습니다.

`Context (맥락)`:

- 관련 프로젝트 상황, 기존 구조, 운영 방식, 제약을 적습니다.
- 배경보다 현재 판단에 필요한 주변 정보를 담습니다.

`Constraints (제약)`:

- 반드시 지켜야 하는 조건을 적습니다.
- 예: 기존 변경사항을 되돌리지 않음, 자동화 도입 제외, 계약 경계 변경은 승인 필요.

`Options (대안)`:

- 가능한 선택지를 나열합니다.
- 각 옵션은 짧은 이름과 설명을 갖는 편이 좋습니다.

`Trade-offs (트레이드오프)`:

- 각 대안의 장점, 단점, 비용, 리스크를 적습니다.
- 추천안의 이유를 분명히 하기 위한 섹션입니다.

`Decision Candidate (결정 후보)`:

- 아직 확정 전이지만 현재 가장 유력한 결론을 적습니다.
- 사용자 승인 전까지는 확정 표현을 피합니다.

`Open Issues (열린 쟁점)`:

- 답변이 없거나 후속 논의가 필요한 쟁점을 적습니다.
- `Questions (질문)`보다 넓은 미해결 사항을 둘 수 있습니다.

`Resolution (정리 결과)`:

- 논의가 닫힐 때 최종 결론과 반영 결과를 적습니다.
- 어떤 공식 문서로 흡수됐는지 함께 적습니다.

`Absorption Target (흡수 대상)`:

- 논의 결과가 어디로 흡수될지 적습니다.
- 예: `docs/contracts/001-api-boundaries.md`, `docs/plans/open/...`, `AGENTS.md`.

## README 반영 방식 제안

`docs/plans/README.md`에는 다음 구성이 적합합니다.

- 목적
- 상태 디렉토리 설명
- 파일명 규칙
- 상태와 디렉토리 일치 규칙
- 체크리스트 상태 값
- 필수 섹션 설명
- 권장 섹션 설명
- 문서 목록: scheduled, open, closed

`.opencode-context/discussions/README.md`에는 다음 구성이 적합합니다.

- 목적
- 상태 디렉토리 설명
- 파일명 규칙
- 상태와 디렉토리 일치 규칙
- closed 논의의 공식 문서 흡수 규칙
- 필수 섹션 설명
- 권장 섹션 설명
- 문서 목록: draft, open, closed

## 루트 논의 문서 이동 제안

현재 루트의 `docs-context-restructure-discussion.md`는 승인 후 다음 경로로 이동하는 것을 권장합니다.

```text
.opencode-context/discussions/closed/2026-06-13_000000_docs-context-restructure.md
```

다만 정확한 최초 생성 시각을 파일 시스템에서 신뢰하기 어렵다면, 이번 대화 날짜 기준으로 다음처럼 저장해도 충분합니다.

```text
.opencode-context/discussions/closed/2026-06-13_000000_docs-context-restructure.md
```

이동 시 본문도 새 논의 문서 스타일에 맞춰 최소 갱신하는 편이 좋습니다.

- `Status (상태)`를 `closed`로 변경합니다.
- `Resolution (정리 결과)`를 추가합니다.
- `Absorption Target (흡수 대상)`에 갱신된 공식 README와 `AGENTS.md`를 적습니다.

## AGENTS.md 정합성 수정 제안

이번 구조 변경 승인 시 `AGENTS.md`에는 다음 수정이 필요합니다.

- `Context Files`에서 `decisions`와 `.opencode-context/contracts` 기준 설명을 제거합니다.
- 계약 문서 기준 위치를 `docs/contracts`로 바꿉니다.
- 아키텍처 문서 기준 위치를 `docs/architectures`로 추가합니다.
- 계획 문서 기준 위치를 `docs/plans`로 추가합니다.
- 논의 문서 위치를 `.opencode-context/discussions/{draft|open|closed}/`로 바꿉니다.
- `Architecture Discussions`에서 확정 결론은 `docs/contracts`, `docs/architectures`, `docs/plans`, README 등으로 흡수한다고 설명합니다.
- `Contract Boundaries`에서 계약 문서 우선 기준을 `docs/contracts`로 바꿉니다.
- 중복된 `Graphify Policy` 섹션은 하나로 합칩니다.

## 남은 판단 지점

아직 결정하면 좋은 지점은 다음과 같습니다.

- 계획 문서와 논의 문서에서 권장 섹션의 순서를 README 템플릿에 그대로 고정할지, 필요한 섹션만 선택하도록 할지 결정해야 합니다.
- 루트 논의 문서 이동 시 파일명 시간을 `000000`으로 둘지, 실제 이동 시각을 쓸지 결정해야 합니다.
- `closed` 논의 문서가 공식 문서 흡수를 증명하기 위해 `Absorption Target (흡수 대상)`을 필수로 둘지 결정해야 합니다.

## 권장 결정

다음 결정을 권장합니다.

- 권장 섹션은 README에 설명하되 문서마다 필요한 것만 선택하게 합니다.
- 필수 섹션 순서는 README 템플릿에서 고정합니다.
- `closed` 논의 문서에는 `Resolution (정리 결과)`와 `Absorption Target (흡수 대상)`을 사실상 필수처럼 요구합니다.
- 루트 논의 문서 이동 파일명은 `2026-06-13_000000_docs-context-restructure.md`로 둡니다.
