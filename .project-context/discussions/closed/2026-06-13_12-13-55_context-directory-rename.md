# Discussion: context 디렉토리 이름 변경

## Status (상태)

closed

## Summary (요약)

현재 `.opencode-context/`는 opencode 전용 설정이 아니라 프로젝트 작업 맥락, 논의, 보고서, 세션, 입력 자료, 보존 자료를 담는 공간입니다. 의미상 특정 도구 이름인 `opencode`에 묶는 것보다 `.project-context/`처럼 프로젝트 중심 이름으로 바꾸는 것이 더 자연스럽습니다.

최종 결론은 `.opencode-context/`를 `.project-context/`로 변경하는 것입니다. 다만 경로가 `AGENTS.md`, `opencode.json`, `.gitignore`, README, 보고서, 계획서, 논의 문서, 세션 문서 전체에 넓게 퍼져 있으므로 단순 디렉토리 rename이 아니라 경로 정책 전체 정합성 수정으로 다룹니다.

## Background (배경)

최근 문서 구조 개편으로 공식 문서는 `docs/`에 두고, 작업 중 맥락은 `.opencode-context/`에 두는 구조로 정리했습니다. 이 과정에서 `.opencode-context/contracts`와 `.opencode-context/decisions`는 제거했고, `.opencode-context/`에는 다음 성격의 자료가 남았습니다.

- 보고서
- 논의 문서
- 세션 체크포인트
- 사용자 제공 임시 입력 자료
- 장기 보존할 작업 자료

이제 `.opencode-context/`는 opencode 설정 자체가 아니라 프로젝트 협업 맥락 저장소에 가깝습니다. 따라서 이름이 실제 책임보다 좁고 도구 종속적으로 보일 수 있습니다.

## Context (맥락)

현재 공식 문서 구조는 다음과 같습니다.

- `docs/contracts/`: 공식 계약 경계 문서
- `docs/architectures/`: 공식 아키텍처 문서
- `docs/plans/`: 공식 계획 문서

현재 작업 맥락 구조는 다음과 같습니다.

- `.opencode-context/reports/`: 분석 보고서, 검토 결과, 제안서
- `.opencode-context/discussions/`: 초안, 진행 중, 종료된 논의 문서
- `.opencode-context/sessions/`: 세션 체크포인트와 인계 메모
- `.opencode-context/inbox/`: 사용자 제공 임시 입력 자료
- `.opencode-context/assets/`: 보존 자료

현재 확인한 직접 영향 범위는 다음과 같습니다.

- Markdown 문서에서 `.opencode-context` 언급이 다수 존재합니다.
- `opencode.json` command template에 `.opencode-context/sessions/`와 `.opencode-context/discussions/draft/`가 들어 있습니다.
- `.gitignore`에 `.opencode-context/inbox/**` 및 예외 규칙이 들어 있습니다.
- `AGENTS.md`의 Context Files, User Input Files, Architecture Discussions, Environment Setup 지침에 해당 경로가 들어 있습니다.

## Scope (범위)

포함:

- `.opencode-context/`의 새 이름 후보 평가
- 의미상 가장 적합한 이름 추천
- 이름 변경 시 수정해야 하는 전체 경로 범위 정리
- 구현 시 안전한 순서 제안
- 이전 히스토리 문서에 남아 있는 경로를 어떻게 다룰지 판단

제외:

- 이번 논의 문서 작성 단계에서는 실제 디렉토리 rename을 하지 않습니다.
- `docs/` 구조 자체는 바꾸지 않습니다.
- opencode 공식 config 위치 문제는 별도 주제로 다룹니다. 현재 결론은 프로젝트 config는 루트 `opencode.json|jsonc`가 공식 권장 위치입니다.

## Constraints (제약)

- 공식 문서와 작업 맥락의 책임 경계는 유지합니다.
- 이름 변경 후에도 `opencode.json` command가 유효해야 합니다.
- `.gitignore`의 inbox 임시 자료 ignore 정책은 유지하되 `.gitkeep` 예외는 유지해야 합니다.
- 기존 완료된 보고서, 계획서, 논의 문서는 과거 사실을 담고 있으므로 모든 경로를 무조건 현재 경로로 바꾸면 히스토리가 왜곡될 수 있습니다.
- 현재 작업 트리에는 `.gitkeep` 추가와 `.gitignore` 수정이 아직 커밋되지 않은 상태입니다.

## Analysis (분석)

`.opencode-context`의 장점:

- opencode와 함께 만들어진 작업 맥락임이 드러납니다.
- 현재 opencode 지침과 연결된다는 점이 명확합니다.

`.opencode-context`의 단점:

- opencode 전용 설정 디렉토리처럼 오해될 수 있습니다.
- 다른 에이전트, 다른 도구, 사람 협업 문서로 확장하기 어색합니다.
- 현재 실제 내용은 프로젝트 맥락 저장소인데 이름은 특정 도구에 종속되어 있습니다.

`.project-context`의 장점:

- 프로젝트 작업 맥락이라는 의미가 가장 직접적입니다.
- 특정 도구에 종속되지 않습니다.
- `docs/`와 역할이 잘 나뉩니다. `docs/`는 공식 문서, `.project-context/`는 작업 맥락입니다.
- 템플릿으로 재사용할 때 opencode 외 도구에도 자연스럽습니다.

`.project-context`의 단점:

- opencode와 직접 연결되는 이름은 아니므로, opencode command와 지침에서 이 디렉토리를 명확히 설명해야 합니다.
- 기존 `.opencode-context` 경로를 참조하는 과거 문서와 외부 습관을 갱신해야 합니다.

이름 변경은 단순 cosmetic 변경이 아닙니다. `opencode.json`, `AGENTS.md`, `.gitignore`, README, 문서 내부 참조, 세션/보고서/계획/논의의 문서 목록에 영향을 줍니다.

## Options (대안)

옵션 A: `.opencode-context` 유지

- 변경 비용이 없습니다.
- opencode 전용 맥락이라는 의미는 유지됩니다.
- 다만 현재 책임보다 이름이 좁습니다.

옵션 B: `.project-context`로 변경

- 프로젝트 작업 맥락 저장소라는 의미가 가장 명확합니다.
- 도구 독립적입니다.
- 현재 구조와 장기 방향에 가장 잘 맞습니다.

옵션 C: `.agent-context`로 변경

- 에이전트 협업 맥락이라는 의미가 명확합니다.
- opencode 종속성은 줄어듭니다.
- 다만 사람이 직접 관리하는 프로젝트 맥락이라는 의미는 `.project-context`보다 약합니다.

옵션 D: `.workspace-context`로 변경

- 작업공간 단위 맥락이라는 의미가 있습니다.
- IDE workspace나 monorepo workspace와 혼동될 수 있습니다.

옵션 E: `.ai-context`로 변경

- AI 협업 공간이라는 의미는 명확합니다.
- 다소 유행어처럼 보이고, 사람 중심 문서의 의미가 약합니다.

## Trade-offs (트레이드오프)

옵션 A는 변경 비용이 가장 낮지만 의미 정합성이 떨어집니다.

옵션 B는 변경 비용이 있지만 장기적인 이름 안정성과 도구 독립성이 가장 좋습니다.

옵션 C는 AI/agent 협업이라는 목적은 잘 드러내지만, 프로젝트 전체 작업 맥락이라는 넓은 책임에는 다소 좁습니다.

옵션 D는 중립적이지만 `workspace`라는 용어가 git project root와 다르게 해석될 수 있습니다.

옵션 E는 짧고 명확하지만 너무 AI 중심이라 공식 문서와 사람 협업 맥락을 담기에는 가볍게 보일 수 있습니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안은 옵션 B, `.project-context`입니다.

추천 구현 방향:

- `.opencode-context/`를 `.project-context/`로 이동합니다.
- `AGENTS.md`의 모든 context 경로를 `.project-context/`로 변경합니다.
- `opencode.json` command template의 sessions와 discussions 경로를 `.project-context/`로 변경합니다.
- `.gitignore`의 inbox ignore/예외 규칙을 `.project-context/inbox/**` 기준으로 변경합니다.
- `.project-context/README.md` 첫 문장을 “프로젝트 작업 맥락과 에이전트 협업 산출물을 보관하는 디렉토리”로 정의합니다.
- 현재 정책 문서와 README의 경로는 새 경로로 갱신합니다.
- 과거 완료 보고서/계획서/논의 문서의 역사적 설명은 원칙적으로 보존하되, 문서 상단에 “현재 경로는 `.project-context/`”라는 갱신 메모를 넣는 방식을 고려합니다.

## Decision Candidate (결정 후보)

채택된 결정:

- `.opencode-context/`를 `.project-context/`로 변경합니다.
- 새 공식 정의는 “프로젝트 작업 맥락과 에이전트 협업 산출물을 보관하는 디렉토리”로 합니다.
- `docs/`는 계속 공식 문서 위치로 둡니다.

## Questions (질문)

- 새 이름은 `.project-context`로 확정했습니다.
- 과거 완료 문서의 본문 경로는 역사적 설명 보존을 위해 일괄 치환하지 않습니다.
- `.opencode-context`에서 `.project-context`로 이동한 뒤, 이전 경로 호환을 위한 symlink나 안내 파일 없이 완전히 제거합니다.
- `.gitkeep` 정리 변경과 이 논의 초안은 먼저 커밋했고, rename 구현은 별도 계획 승인 후 진행합니다.

## Open Issues (열린 쟁점)

현재 없음.

## Resolution (정리 결과)

이 논의의 결론은 `docs/plans/scheduled/2026-06-13_12-18-13_context-directory-rename.md` 계획서로 흡수했습니다.

최종 결정:

- 작업 맥락 디렉토리 이름은 `.project-context`로 변경합니다.
- 과거 완료 문서의 역사적 `.opencode-context` 본문 설명은 보존합니다.
- 이전 `.opencode-context` 경로에는 symlink나 안내 파일을 남기지 않습니다.
- 구현은 계획서 승인 후 진행합니다.

## Absorption Target (흡수 대상)

- `docs/plans/scheduled/2026-06-13_12-18-13_context-directory-rename.md`
- `docs/plans/README.md`

## References (근거 및 영향 문서)

근거:

- `AGENTS.md`
- `opencode.json`
- `.gitignore`
- `.opencode-context/README.md`
- `.opencode-context/discussions/README.md`
- `.opencode-context/reports/README.md`
- `.opencode-context/sessions/README.md`
- `.opencode-context/assets/README.md`
- `docs/plans/closed/2026-06-13_11-28-02_docs-context-restructure.md`
- `.opencode-context/discussions/closed/2026-06-13_11-38-21_docs-context-restructure.md`
- `docs/plans/scheduled/2026-06-13_12-18-13_context-directory-rename.md`

영향:

- `.opencode-context/` 전체 경로
- `.project-context/` 신규 경로
- `AGENTS.md`
- `opencode.json`
- `.gitignore`
- `docs/README.md`
- `docs/plans/README.md`
- `docs/plans/closed/2026-06-13_11-28-02_docs-context-restructure.md`
- `.opencode-context/reports/007-current-opencode-state.md`
- `.opencode-context/reports/008-docs-context-structure-consistency.md`
- `.opencode-context/reports/009-plan-discussion-section-policy.md`
