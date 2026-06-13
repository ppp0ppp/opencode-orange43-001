# Discussions (논의)

opencode와 사용자가 결정 전 사고 과정, 질문/답변, 대안, 트레이드오프를 정리하는 위치입니다.

논의가 끝난 결론은 별도 decisions 디렉토리에 두지 않고 `docs/contracts`, `docs/architectures`, `docs/plans`, 관련 README, `AGENTS.md` 등 공식 문서로 흡수합니다.

## Status Directories (상태 디렉토리)

- `draft/`: 초안, 미정의 주제, 에이전트가 먼저 제안한 문서
- `open/`: 사용자와 에이전트가 질문/답변과 수정으로 완성 중인 문서
- `closed/`: 논의가 끝났고 공식 문서로 흡수된 문서

논의 문서의 디렉토리 상태와 본문 `Status (상태)`는 항상 일치해야 합니다. 상태 이동 시 파일명은 바꾸지 않고 최초 생성 시각을 유지합니다.

## Naming (이름 규칙)

논의 문서는 상태 이동과 시간 추적성이 중요하므로 최초 생성 시각을 기준으로 다음 형식을 사용합니다.

```text
YYYY-MM-DD_HH-MM-SS_detail-title.md
```

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

`References (근거 및 영향 문서)`:

- 논의의 근거 문서와 영향을 받을 문서를 적습니다.

## Documents (문서 목록)

Draft:

- 현재 없음

Open:

- 현재 없음

Closed:

- `closed/2026-06-13_11-38-21_docs-context-restructure.md`: docs 및 `.opencode-context` 문서 구조 재조정
