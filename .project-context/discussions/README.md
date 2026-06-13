# Discussions (논의)

사용자와 에이전트가 결정 전 사고 과정, 질문/답변, 대안, 트레이드오프를 정리하는 위치입니다.

논의가 끝난 결론은 별도 decisions 디렉토리에 두지 않고 `docs/contracts`, `docs/architectures`, `docs/plans`, 관련 README, `AGENTS.md` 등 공식 문서로 흡수합니다.

## Status Directories (상태 디렉토리)

- `draft/`: 초안, 미정의 주제, 에이전트가 먼저 제안한 문서
- `open/`: 사용자와 에이전트가 질문/답변과 수정으로 완성 중인 문서
- `closed/`: 논의가 끝났고 공식 문서로 흡수된 문서

계획 작성 중에는 `draft/`와 `open/` 논의를 기본 참조할 수 있습니다. `closed/` 논의는 히스토리와 근거이며, 사용자가 명시하거나 에이전트가 참조 이유를 설명해 승인받은 경우에만 참조합니다.

논의 문서의 디렉토리 상태와 본문 `Status (상태)`는 항상 일치해야 합니다. 상태 이동 시 파일명은 바꾸지 않고 최초 생성 시각을 유지합니다.

## Naming (이름 규칙)

논의 문서는 상태 이동과 시간 추적성이 중요하므로 최초 생성 시각을 기준으로 다음 형식을 사용합니다.

```text
YYYY-MM-DD_HH-MM-SS_detail-title.md
```

대형 논의는 상태 디렉토리 바로 아래에 다음 형식의 디렉토리로 둡니다.

```text
YYYY-MM-DD_HH-MM-SS_detail-title/
```

대형 논의 디렉토리는 `main-discussion.md`를 기준 문서로 사용합니다. 대형 논의 디렉토리의 외부 상태는 `main-discussion.md`의 `Status (상태)`를 따릅니다.

## Large Discussions (대형 논의)

대형 논의는 다음 구조를 사용합니다.

```text
.project-context/discussions/open/2026-06-13_13-17-01_large-topic/
  main-discussion.md
  draft/
    2026-06-13_13-20-00_sub-topic-a.md
  open/
    2026-06-13_13-25-00_sub-topic-b.md
  closed/
    2026-06-13_13-30-00_sub-topic-c.md
```

- 일반 논의는 상태 디렉토리 바로 아래 `.md` 파일로 둡니다.
- 대형 논의는 상태 디렉토리 바로 아래 디렉토리로 둡니다.
- 대형 논의의 내부 상태 디렉토리는 `draft/`, `open/`, `closed/`만 사용합니다.
- 하위 논의의 상태는 대형 논의 내부 상태 디렉토리와 본문 `Status (상태)`를 따릅니다.
- 하위 논의는 한 단계만 허용하며 하위 논의 아래에 다시 하위 논의 디렉토리를 만들지 않습니다.
- 하위 논의 목록과 진행 관리는 `main-discussion.md`에서 합니다.
- README 문서 목록은 상태 디렉토리 바로 아래의 일반 논의와 대형 논의 디렉토리까지만 나열합니다.

## Required Sections (필수 섹션)

논의 문서는 아래 섹션 순서를 고정합니다. 특정 문서에서 필요하지 않은 섹션도 삭제하지 않고 `사용하지 않음` 또는 `현재 없음`으로 명시합니다.

`Status (상태)`:

- 현재 논의 문서의 상태를 적습니다.
- 허용 값은 `draft`, `open`, `closed`입니다.

`Summary (요약)`:

- 논의 주제와 현재 결론을 짧게 적습니다.
- `open` 상태에서는 현재 선호안을 적고, `closed` 상태에서는 최종 흡수 결과를 적습니다.

`Background (배경)`:

- 왜 이 논의가 시작됐는지 적습니다.

`Context (맥락)`:

- 관련 프로젝트 상황, 기존 구조, 운영 방식, 제약을 적습니다.

`Scope (범위)`:

- 본 논의가 다루는 주제와 다루지 않는 주제를 적습니다.

`Constraints (제약)`:

- 반드시 지켜야 하는 조건을 적습니다.

`Analysis (분석)`:

- 현재 상태, 문제, 관찰, 리스크를 적습니다.

`Options (대안)`:

- 가능한 선택지를 나열합니다.

`Trade-offs (트레이드오프)`:

- 각 대안의 장점, 단점, 비용, 리스크를 적습니다.

`Recommended Strategy / Plan / Options (추천 전략/계획/옵션)`:

- 추천 전략, 실행 계획, 또는 선택 가능한 대안을 적습니다.

`Decision Candidate (결정 후보)`:

- 아직 확정 전이지만 현재 가장 유력한 결론을 적습니다.

`Questions (질문)`:

- 사용자 판단이 필요한 질문을 적습니다.

`Open Issues (열린 쟁점)`:

- 답변이 없거나 후속 논의가 필요한 쟁점을 적습니다.

`Resolution (정리 결과)`:

- 논의가 닫힐 때 최종 결론과 반영 결과를 적습니다.

`Absorption Target (흡수 대상)`:

- 논의 결과가 어디로 흡수됐는지 적습니다.
- `closed` 논의 문서에서는 필수입니다.
- `closed` 논의 문서는 실행 기준이 아니므로, 계속 필요한 결론은 공식 문서나 계획서로 흡수되어 있어야 합니다.

`References (근거 및 영향 문서)`:

- 논의의 근거 문서와 영향을 받을 문서를 적습니다.

## Documents (문서 목록)

Draft:

- 현재 없음

Open:

- 현재 없음

Closed:

- `.project-context/discussions/closed/2026-06-13_11-38-21_docs-context-restructure.md`: docs 및 `.opencode-context` 문서 구조 재조정
- `.project-context/discussions/closed/2026-06-13_12-13-55_context-directory-rename.md`: context 디렉토리 이름 변경
- `.project-context/discussions/closed/2026-06-13_12-49-18_path-reference-style.md`: 문서 경로 표기 방식
- `.project-context/discussions/closed/2026-06-13_13-17-01_large-work-breakdown-tracking.md`: 대형 작업의 논의와 계획 분할 관리
- `.project-context/discussions/closed/2026-06-13_14-02-12_execution-authority-workflow.md`: 실행 권한 계층과 README 워크플로우 표현
- `.project-context/discussions/closed/2026-06-13_14-43-44_plan-tree-checklist-readability.md`: Plan Tree와 체크리스트 가독성 개선
- `.project-context/discussions/closed/2026-06-13_15-20-02_project-local-permission-allowlist.md`: 프로젝트 로컬 권한 allowlist 조정
- `.project-context/discussions/closed/2026-06-13_15-42-07_planning-web-access-policy.md`: 논의/계획 단계 웹 접근 정책
