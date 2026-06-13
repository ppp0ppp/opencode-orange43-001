# Discussion: 문서 경로 표기 방식

## Status (상태)

closed

## Summary (요약)

프로젝트 문서에서 경로를 표기할 때 문서 위치 기준 상대 경로와 `docs/...`, `.project-context/...` 같은 프로젝트 루트 기준 경로 중 무엇을 기본으로 삼을지 논의합니다.

최종 결론은 프로젝트 문서의 모든 경로 표기를 프로젝트 루트 기준 경로로 강제하는 것입니다. 문서 목록에서도 짧은 상대 경로를 사용하지 않고, Markdown 클릭 링크 병기도 기본적으로 사용하지 않습니다.

## Background (배경)

문서 구조를 `docs/`와 `.project-context/` 중심으로 재정리하면서 여러 문서가 서로를 참조하게 되었습니다. 계획서와 논의 문서는 `scheduled`, `open`, `closed` 상태 디렉토리 사이를 이동하고, `.project-context/` 문서도 추후 이름이나 위치가 바뀔 수 있습니다.

이 상황에서 문서 위치 기준 상대 링크는 클릭 가능성은 좋지만, 문서 이동 시 쉽게 깨질 수 있습니다. 반대로 `docs/...` 같은 루트 기준 경로는 Markdown 렌더러에서 자동 링크가 되지 않을 수 있지만 사람이 읽고 검색하기 좋습니다.

## Context (맥락)

현재 프로젝트의 주요 문서 위치는 다음과 같습니다.

- `docs/contracts/`
- `docs/architectures/`
- `docs/plans/{scheduled|open|closed}/`
- `.project-context/discussions/{draft|open|closed}/`
- `.project-context/reports/`
- `.project-context/sessions/`
- `.project-context/inbox/`
- `.project-context/assets/`

현재 문서에서 경로는 대체로 루트 기준으로 쓰이고 있습니다.

예시:

- `docs/contracts/README.md`
- `.project-context/discussions/closed/2026-06-13_12-13-55_context-directory-rename.md`
- `docs/plans/closed/2026-06-13_12-18-13_context-directory-rename.md`

일부 README에는 해당 README 기준의 짧은 경로가 있었지만, 최종 정책에서는 허용하지 않습니다.

예시:

- `closed/2026-06-13_12-18-13_context-directory-rename.md`
- `scheduled/2026-06-13_12-18-13_context-directory-rename.md`

## Scope (범위)

포함:

- 문서 본문에서 경로를 표기하는 기본 방식
- README 문서 목록에서 경로를 표기하는 방식
- 실제 Markdown 링크가 필요한 경우의 예외 규칙
- 계획서, 논의 문서처럼 이동 가능한 문서에 적합한 경로 규칙

제외:

- 이번 논의 문서 작성 단계에서는 기존 문서의 경로를 일괄 수정하지 않습니다.
- 파일 시스템 구조는 변경하지 않습니다.
- 자동 링크 검사 도구나 문서 빌드 도구는 도입하지 않습니다.

## Constraints (제약)

- 계획서와 논의 문서는 상태 디렉토리 사이를 이동할 수 있습니다.
- 문서 본문은 사람과 에이전트가 grep/search로 빠르게 찾을 수 있어야 합니다.
- 일부 문서는 GitHub Markdown에서 클릭 가능한 링크가 있으면 편합니다.
- 과거 완료 문서의 역사적 경로 설명은 보존할 수 있습니다.
- 경로 규칙은 `AGENTS.md`, `docs/plans/README.md`, `.project-context/discussions/README.md`와 충돌하지 않아야 합니다.

## Analysis (분석)

프로젝트 루트 기준 경로의 장점:

- 문서가 다른 디렉토리로 이동해도 경로 의미가 유지됩니다.
- `docs/...`, `.project-context/...`처럼 프로젝트 안 위치가 바로 보입니다.
- grep/search 결과가 일관됩니다.
- 에이전트와 사용자가 같은 workspace root에서 작업할 때 해석이 쉽습니다.
- 계획서와 논의 문서처럼 이동 가능한 문서에 특히 안전합니다.

프로젝트 루트 기준 경로의 단점:

- Markdown에서 기본적으로 클릭 가능한 링크가 아닐 수 있습니다.
- GitHub Markdown 링크로 쓰려면 문서 위치 기준 링크 대상을 별도로 관리해야 할 수 있습니다.

문서 위치 기준 상대 링크의 장점:

- GitHub Markdown에서 클릭 가능한 링크를 만들기 쉽습니다.
- 같은 디렉토리나 인접 디렉토리의 문서 목록에는 짧고 간결합니다.

문서 위치 기준 상대 링크의 단점:

- 문서가 이동하면 링크가 깨질 수 있습니다.
- 상위 디렉토리 이동 표기가 많아지면 사람이 실제 위치를 파악하기 어렵습니다.
- 상태 디렉토리를 오가는 계획서와 논의 문서에는 유지 비용이 큽니다.

## Options (대안)

옵션 A: 모든 경로를 프로젝트 루트 기준으로 표기

- 예: `docs/contracts/README.md`
- 예: `.project-context/reports/008-docs-context-structure-consistency.md`

옵션 B: 모든 경로를 문서 위치 기준 상대 링크로 표기

- 예: 문서 위치에 따라 달라지는 상대 경로
- 예: 다른 디렉토리로 이동하면 깨지는 링크 대상

옵션 C: 본문은 루트 기준, 클릭 링크가 필요한 곳만 상대 링크 사용

- 예: 본문 경로는 `docs/contracts/README.md`
- 예: 클릭 링크는 별도 Markdown 링크 대상으로 둡니다.

옵션 D: README 문서 목록은 해당 README 기준 짧은 상대 경로, 본문과 정책은 루트 기준 경로 사용

- 예: `docs/plans/README.md`의 목록에는 `closed/2026-...md`
- 예: 다른 문서에서 참조할 때는 `docs/plans/closed/2026-...md`

## Trade-offs (트레이드오프)

옵션 A는 가장 일관되고 검색에 강하지만 클릭 가능한 링크성이 약합니다.

옵션 B는 링크 UX는 좋지만 문서 이동에 취약하고, 깊은 디렉토리에서는 가독성이 나쁩니다.

옵션 C는 가장 실용적입니다. 기본 표기는 루트 기준으로 안정성을 얻고, 링크가 필요한 곳만 상대 링크를 병행합니다.

옵션 D는 README 문서 목록의 간결성을 살릴 수 있지만, “본문/정책”과 “목록”의 규칙이 달라진다는 점을 명시해야 합니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

채택된 추천안은 옵션 A입니다.

확정 규칙:

- 본문, 계획서, 논의 문서, 보고서, `AGENTS.md`, `opencode.json` 설명에서는 프로젝트 루트 기준 경로를 사용합니다.
- README의 문서 목록에서도 프로젝트 루트 기준 경로를 사용합니다.
- Markdown 클릭 링크는 기본적으로 사용하지 않습니다.
- 문서 위치 기준 상대 경로 형식은 기본 표기 방식으로 쓰지 않습니다.

예시:

```md
근거 문서: `docs/plans/closed/2026-06-13_12-18-13_context-directory-rename.md`
```

사용하지 않는 방식:

```md
`docs/plans/closed/2026-06-13_12-18-13_context-directory-rename.md`
```

README 목록에서도 다음처럼 루트 기준 전체 상대 경로를 사용합니다.

```md
- `docs/plans/closed/2026-06-13_12-18-13_context-directory-rename.md`: context 디렉토리 이름 변경
```

## Decision Candidate (결정 후보)

채택된 결정:

- 경로 표기의 기본은 프로젝트 루트 기준으로 합니다.
- README 문서 목록도 프로젝트 루트 기준 경로로 강제합니다.
- Markdown 클릭 링크 병기는 기본적으로 사용하지 않습니다.
- 문서 위치 기준 상대 경로 형식은 기본 표기 방식으로 쓰지 않습니다.

## Questions (질문)

- 프로젝트 문서 표준으로 확정했습니다.
- `docs/plans/README.md`와 `.project-context/discussions/README.md`의 문서 목록도 짧은 상대 경로를 허용하지 않습니다.
- 클릭 링크 병기는 필요하지 않은 것으로 결정했습니다.
- 규칙은 우선 `AGENTS.md`에 명시합니다.

## Open Issues (열린 쟁점)

현재 없음.

## Resolution (정리 결과)

이 논의의 결론은 `docs/plans/scheduled/2026-06-13_12-55-02_path-reference-style.md` 계획서로 흡수했습니다.

최종 결정:

- 프로젝트 문서의 경로 표기는 프로젝트 루트 기준 경로로 강제합니다.
- README 문서 목록에서도 짧은 상대 경로를 사용하지 않습니다.
- Markdown 클릭 링크 병기는 기본적으로 사용하지 않습니다.
- 우선 `AGENTS.md`에 이 규칙을 명시합니다.

## Absorption Target (흡수 대상)

- `AGENTS.md`
- `docs/plans/scheduled/2026-06-13_12-55-02_path-reference-style.md`

## References (근거 및 영향 문서)

근거:

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`
- `.project-context/reports/README.md`
- `docs/plans/closed/2026-06-13_12-18-13_context-directory-rename.md`

영향:

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`
- `.project-context/README.md`
- 향후 작성되는 `docs/plans/{scheduled|open|closed}/` 문서
- 향후 작성되는 `.project-context/discussions/{draft|open|closed}/` 문서
- 향후 작성되는 `.project-context/reports/` 문서
