# Discussion: docs 및 .opencode-context 문서 구조 재조정

## Status (상태)

closed

## Summary (요약)

프로젝트 문서 구조를 `docs/` 중심으로 재배치하고, `.opencode-context/`를 opencode와 사용자 간의 작업 맥락 공간으로 축소하는 논의입니다.

최종적으로 계약, 아키텍처, 계획 문서는 `docs/`에 두고, 논의, 보고서, 세션, 입력 자료는 `.opencode-context/`에 두는 방향으로 정리했습니다.

## Background (배경)

기존 구조에서는 `.opencode-context/decisions`, `.opencode-context/contracts`, `.opencode-context/discussions`가 함께 존재했습니다. 이 중 계약 문서와 확정 결정 기록은 프로젝트 공식 문서와 중복되거나 숨김 디렉토리에 위치하는 문제가 있었습니다.

사용자는 `.opencode-context/decisions` 삭제, `.opencode-context/contracts`의 `docs/contracts` 이동, `docs/architectures`, `docs/plans`, 상태 기반 discussions 구조 추가를 제안했습니다.

## Context (맥락)

이 프로젝트는 opencode 기본 설정 템플릿으로도 사용됩니다. 따라서 실제 문서 경로뿐 아니라 `AGENTS.md`의 작업 지침도 새 구조와 일치해야 합니다.

## Scope (범위)

포함:

- `.opencode-context/decisions` 삭제 여부와 영향 정리
- `.opencode-context/contracts`를 `docs/contracts`로 이동하는 방안
- `docs/architectures` 신설 방안
- `docs/plans` 및 `scheduled`, `doing`, `archived` 하위 상태 디렉토리 신설 방안
- `.opencode-context/discussions`를 `draft`, `open`, `closed` 하위 상태 디렉토리로 재정렬하는 방안
- README와 `AGENTS.md` 정합성 수정 방안

제외:

- 문서 자동 생성기 또는 CI 도입
- graphify hook 또는 생성물 관리 변경
- 제품 기능 또는 런타임 코드 변경

## Constraints (제약)

- 공식 문서와 opencode 작업 맥락은 분리합니다.
- `reports`와 `sessions`는 `.opencode-context/` 아래에 유지합니다.
- `contracts`와 `architectures`는 압축성과 순서 유지를 위해 `001-short-title.md` 형식을 사용합니다.
- `plans`와 `discussions`는 상태 이동과 시간 추적성을 위해 `YYYY-MM-DD_HH-MM-SS_detail-title.md` 형식을 사용합니다.
- README 문서 목록은 수동으로 관리합니다.

## Analysis (분석)

- `.opencode-context/decisions`는 `docs/contracts`, `docs/architectures`, `docs/plans`와 중복될 수 있습니다.
- `.opencode-context/contracts`는 프로젝트 공식 계약 문서 성격이 강하므로 `docs/contracts`가 더 적합합니다.
- 계획 문서는 승인 전, 실행 중, 완료 상태를 추적할 공식 위치가 필요합니다.
- 논의 문서는 초안, 진행 중, 종료 상태를 디렉토리와 본문 상태로 함께 표현하는 편이 명확합니다.
- `AGENTS.md`의 기존 경로 정책을 수정하지 않으면 새 구조와 에이전트 지침이 충돌합니다.

## Options (대안)

- 옵션 A: `.opencode-context/decisions`를 유지하고 공식 문서와 상호 참조합니다.
- 옵션 B: `.opencode-context/decisions`를 삭제하고 확정 판단을 공식 문서로 흡수합니다.
- 옵션 C: 모든 문서를 `docs/`로 옮기고 `.opencode-context/`를 없앱니다.

## Trade-offs (트레이드오프)

- 옵션 A는 과거 ADR 방식에 익숙하지만 문서가 분산됩니다.
- 옵션 B는 구조가 단순하고 공식 문서 중심성이 좋아지지만, 결정 배경을 README나 공식 문서에 흡수해야 합니다.
- 옵션 C는 공식 문서 위치는 단순해지지만 opencode 작업 맥락과 사용자 제공 임시 자료까지 섞일 위험이 있습니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

옵션 B를 채택합니다.

- `docs/`를 공식 문서 위치로 둡니다.
- `.opencode-context/`는 논의, 보고서, 세션, 입력 자료, 보존 자료 중심으로 유지합니다.
- 확정 판단은 별도 decisions 디렉토리가 아니라 `docs/contracts`, `docs/architectures`, `docs/plans`, 관련 README에 흡수합니다.
- 계획 문서와 논의 문서는 필수 섹션 순서를 고정하고, 사용하지 않는 섹션도 명시적으로 남깁니다.

## Decision Candidate (결정 후보)

채택됨: 공식 문서는 `docs/`, 작업 맥락은 `.opencode-context/`로 분리합니다.

## Questions (질문)

답변 완료:

- `.opencode-context/decisions/001-opencode-context-directory.md`의 배경은 일부 흡수합니다.
- `contracts`와 `architectures`는 `001-short-title.md`를 사용합니다.
- `plans`와 `discussions`는 `YYYY-MM-DD_HH-MM-SS_detail-title.md`를 사용합니다.
- README 문서 목록은 수동 관리합니다.
- `reports`와 `sessions`는 현재 위치를 유지합니다.
- `AGENTS.md` 정합성 수정과 중복 `Graphify Policy` 병합을 포함합니다.
- `docs/plans/scheduled`는 미승인 계획과 승인됐지만 아직 착수하지 않은 계획을 모두 포함합니다.

## Open Issues (열린 쟁점)

현재 없음.

## Resolution (정리 결과)

논의 결과는 실행 계획서와 공식 README, `AGENTS.md` 갱신으로 흡수했습니다.

실행 계획서는 `docs/plans/archived/2026-06-13_11-28-02_docs-context-restructure.md`에 작성했고, 실제 구조 개편 승인 후 완료했습니다.

## Absorption Target (흡수 대상)

- `docs/README.md`
- `docs/contracts/README.md`
- `docs/architectures/README.md`
- `docs/plans/README.md`
- `.opencode-context/README.md`
- `.opencode-context/discussions/README.md`
- `.opencode-context/reports/README.md`
- `.opencode-context/sessions/README.md`
- `.opencode-context/assets/README.md`
- `AGENTS.md`

## References (근거 및 영향 문서)

근거:

- `.opencode-context/reports/008-docs-context-structure-consistency.md`
- `.opencode-context/reports/009-plan-discussion-section-policy.md`
- `docs/plans/archived/2026-06-13_11-28-02_docs-context-restructure.md`
- `.opencode-context/decisions/001-opencode-context-directory.md`

영향:

- `docs/README.md`
- `docs/contracts/README.md`
- `docs/architectures/README.md`
- `docs/plans/README.md`
- `.opencode-context/README.md`
- `.opencode-context/discussions/README.md`
- `AGENTS.md`
