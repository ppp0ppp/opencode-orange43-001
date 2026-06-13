# Plan: docs 및 .opencode-context 문서 구조 재조정

## Status (상태)

closed

이 계획서는 모든 항목이 완료되어 닫힌 계획서입니다.

## Summary (요약)

이 계획은 프로젝트 문서의 공식 위치를 `docs/`로 정리하고, `.opencode-context/`를 opencode와 사용자 간의 작업 맥락, 논의, 보고서, 세션, 입력 자료 중심으로 축소합니다.

핵심 작업은 `.opencode-context/contracts`를 `docs/contracts`로 이동하고, `.opencode-context/decisions`를 삭제하며, `docs/architectures`, `docs/plans`, `.opencode-context/discussions`의 상태 기반 구조를 만드는 것입니다. 또한 `AGENTS.md`와 관련 README의 경로 정책을 새 구조와 일치시킵니다.

## Goal (목표)

- 공식 문서와 작업 중 맥락의 책임 경계를 명확히 합니다.
- 계약, 아키텍처, 계획 문서를 `docs/` 아래에서 장기 관리합니다.
- 논의 문서는 `.opencode-context/discussions/{draft|open|closed}/`에서 상태별로 관리합니다.
- 결정 기록 전용 디렉토리인 `.opencode-context/decisions`를 제거하고 필요한 배경은 공식 README에 흡수합니다.
- `AGENTS.md`의 문서 구조 지침과 실제 파일 구조를 일치시킵니다.

## Scope (작업 범위)

포함:

- `.opencode-context/contracts/`를 `docs/contracts/`로 이동합니다.
- `.opencode-context/decisions/`를 삭제합니다.
- `.opencode-context/decisions/001-opencode-context-directory.md`의 핵심 배경을 `docs/README.md`와 `.opencode-context/README.md`에 흡수합니다.
- `docs/architectures/README.md`를 추가합니다.
- `docs/plans/README.md`와 `scheduled`, `open`, `closed` 하위 디렉토리를 정리합니다.
- `.opencode-context/discussions/README.md`와 `draft`, `open`, `closed` 하위 디렉토리를 정리합니다.
- 루트 `docs-context-restructure-discussion.md`를 `.opencode-context/discussions/closed/`로 이동하고 새 논의 문서 스타일에 맞게 최소 갱신합니다.
- `.opencode-context/reports/README.md`, `.opencode-context/sessions/README.md`, `.opencode-context/assets/README.md`의 `decisions` 또는 예전 `contracts` 경로 언급을 정리합니다.
- `AGENTS.md`의 문서 경로 정책과 중복 `Graphify Policy` 섹션을 정리합니다.
- `opencode.json`의 예전 `decision` command를 새 discussion 구조와 맞게 정리합니다.

제외:

- 문서 자동 리스팅 스크립트 또는 CI 도입은 하지 않습니다.
- 기존 보고서 본문의 의미를 재작성하지 않습니다.
- 계약, 아키텍처, 계획, 논의 문서의 자동 검증 도구는 추가하지 않습니다.
- graphify 생성물 생성 또는 hook 설정은 하지 않습니다.

## Non-Goals (제외 목표)

- 이 계획은 제품 기능, 런타임 코드, 테스트 코드 변경을 다루지 않습니다.
- 이 계획은 문서 구조 정합성에만 집중하며, 각 계약/아키텍처 문서의 실제 도메인 내용을 새로 설계하지 않습니다.
- 이 계획은 보고서 번호 체계 자체를 바꾸지 않습니다.
- 이 계획은 `.opencode-context/reports`, `.opencode-context/sessions`, `.opencode-context/inbox`, `.opencode-context/assets`를 `docs/`로 옮기지 않습니다.

## Assumptions (가정)

- `reports`와 `sessions`는 계속 `.opencode-context/` 아래에 둡니다.
- README 문서 목록은 수동으로 관리합니다.
- `contracts`와 `architectures` 문서 파일명은 `001-short-title.md` 형식을 사용합니다.
- `plans`와 `discussions` 문서 파일명은 최초 생성 시각 기준 `YYYY-MM-DD_HH-MM-SS_detail-title.md` 형식을 사용합니다.
- `docs/plans/scheduled`는 미승인 계획과 승인됐지만 아직 착수하지 않은 계획을 모두 포함합니다.
- 루트 논의 문서를 이동할 때는 실제 이동 시각을 파일명에 사용합니다.

## Dependencies (의존성)

- 이 계획은 `.opencode-context/reports/008-docs-context-structure-consistency.md`와 `.opencode-context/reports/009-plan-discussion-section-policy.md`의 판단에 의존합니다.
- 이 계획은 사용자 승인 후 실행되어야 합니다.
- `AGENTS.md` 수정은 이후 opencode 행동 지침에 영향을 주므로 문서 구조 변경과 같은 작업 단위에서 처리해야 합니다.
- `docs-context-restructure-discussion.md` 이동은 `.opencode-context/discussions/closed/` 디렉토리 생성 이후 수행해야 합니다.

## Risks (리스크)

- `AGENTS.md`를 함께 수정하지 않으면 실제 구조와 에이전트 지침이 충돌합니다.
- `.opencode-context/decisions` 삭제 전에 핵심 배경을 흡수하지 않으면 과거 결정 맥락을 잃을 수 있습니다.
- 상태 디렉토리와 문서 본문 `Status (상태)`가 불일치할 수 있습니다.
- README 문서 목록을 수동 관리하므로 누락될 수 있습니다.
- 루트 논의 문서 이동 시 기존 파일 경로를 참조하는 문서가 있으면 링크가 깨질 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] 기존 문서 구조와 충돌 지점 확인
- [x] 공식 문서 구조 생성 및 이동
- [x] `.opencode-context` 작업 맥락 구조 정리
- [x] 루트 논의 문서 이동 및 종료 처리
- [x] README 정책 및 문서 목록 갱신
- [x] `AGENTS.md` 지침 정합성 수정
- [x] 변경 결과 검증

## Plan Tree (계획 트리)

- [x] 1. 사전 확인
- [x] 1.1. `git status` 확인
- [x] 1.2. 이동/삭제 대상 파일 확인
- [x] 2. `docs/` 공식 문서 구조 정리
- [x] 2.1. `.opencode-context/contracts/`를 `docs/contracts/`로 이동
- [x] 2.2. `docs/contracts/README.md`를 새 정책에 맞게 갱신
- [x] 2.3. `docs/architectures/README.md` 추가
- [x] 2.4. `docs/plans/README.md` 작성
- [x] 2.5. `docs/plans/scheduled`, `docs/plans/open`, `docs/plans/closed` 확인
- [x] 3. `.opencode-context/` 작업 맥락 구조 정리
- [x] 3.1. `.opencode-context/discussions/draft` 추가
- [x] 3.2. `.opencode-context/discussions/open` 추가
- [x] 3.3. `.opencode-context/discussions/closed` 추가
- [x] 3.4. `.opencode-context/discussions/README.md` 갱신
- [x] 3.5. 루트 논의 문서를 `.opencode-context/discussions/closed/`로 이동
- [x] 3.6. `.opencode-context/decisions/`의 핵심 배경 흡수
- [x] 3.7. `.opencode-context/decisions/` 삭제
- [x] 4. 관련 README 정합성 수정
- [x] 4.1. `docs/README.md` 갱신
- [x] 4.2. `.opencode-context/README.md` 갱신
- [x] 4.3. `.opencode-context/reports/README.md` 갱신
- [x] 4.4. `.opencode-context/sessions/README.md` 갱신
- [x] 4.5. `.opencode-context/assets/README.md` 갱신
- [x] 5. `AGENTS.md` 갱신
- [x] 5.1. `Context Files` 지침 갱신
- [x] 5.2. `Architecture Discussions` 지침 갱신
- [x] 5.3. `Contract Boundaries` 지침 갱신
- [x] 5.4. 중복 `Graphify Policy` 섹션 병합
- [x] 5.5. `opencode.json` command 정합성 수정
- [x] 6. 검증
- [x] 6.1. 예전 경로 언급 검색
- [x] 6.2. 문서 구조 확인
- [x] 6.3. `git status` 확인

## Checklist (전체 체크리스트)

- [x] CL-001: 실행 전 `git status` 확인 (done)
- [x] CL-002: `.opencode-context/contracts/`를 `docs/contracts/`로 이동 (done)
- [x] CL-003: `docs/contracts/README.md`를 새 구조에 맞게 갱신 (done)
- [x] CL-004: `docs/architectures/README.md` 추가 (done)
- [x] CL-005: `docs/plans/README.md` 작성 (done)
- [x] CL-006: `docs/plans/scheduled`, `docs/plans/open`, `docs/plans/closed` 상태 디렉토리 확인 또는 추가 (done)
- [x] CL-007: `.opencode-context/discussions/draft`, `.opencode-context/discussions/open`, `.opencode-context/discussions/closed` 상태 디렉토리 추가 (done)
- [x] CL-008: `.opencode-context/discussions/README.md`를 새 섹션 정책으로 갱신 (done)
- [x] CL-009: 루트 `docs-context-restructure-discussion.md`를 실제 이동 시각 파일명으로 `.opencode-context/discussions/closed/`에 이동 (done)
- [x] CL-010: 이동한 논의 문서의 `Status (상태)`, `Resolution (정리 결과)`, `Absorption Target (흡수 대상)` 갱신 (done)
- [x] CL-011: `.opencode-context/decisions/001-opencode-context-directory.md`의 핵심 배경을 `docs/README.md`와 `.opencode-context/README.md`에 흡수 (done)
- [x] CL-012: `.opencode-context/decisions/` 삭제 (done)
- [x] CL-013: `docs/README.md` 갱신 (done)
- [x] CL-014: `.opencode-context/README.md` 갱신 (done)
- [x] CL-015: `.opencode-context/reports/README.md` 갱신 (done)
- [x] CL-016: `.opencode-context/sessions/README.md` 갱신 (done)
- [x] CL-017: `.opencode-context/assets/README.md` 갱신 (done)
- [x] CL-018: `AGENTS.md`의 문서 구조 지침 갱신 (done)
- [x] CL-019: `AGENTS.md`의 중복 `Graphify Policy` 섹션 병합 (done)
- [x] CL-020: 예전 경로 `.opencode-context/contracts`와 `.opencode-context/decisions` 언급 검색 및 필요한 정리 (done)
- [x] CL-021: 변경된 문서 구조와 README 문서 목록 확인 (done)
- [x] CL-022: 최종 `git status` 확인 (done)
- [x] CL-023: `opencode.json`의 `decision` command를 `discussion` command로 변경 (done)

## Verification (검증)

검증 항목:

- `git status --short`로 이동, 삭제, 추가 파일을 확인합니다.
- 텍스트 검색으로 `.opencode-context/contracts`, `.opencode-context/decisions`, `../decisions`, `../contracts`의 잔여 언급을 확인합니다.
- `docs/contracts`, `docs/architectures`, `docs/plans`, `.opencode-context/discussions`의 README가 존재하는지 확인합니다.
- 계획 문서와 논의 문서 README의 필수/권장 섹션 순서가 고정되어 있는지 확인합니다.
- 이동된 루트 논의 문서가 `.opencode-context/discussions/closed/`에 있고 `Status (상태)`가 `closed`인지 확인합니다.
- `AGENTS.md`에 `Graphify Policy` 섹션이 중복되지 않는지 확인합니다.

테스트 명령:

```sh
git status --short
```

문서 작업이므로 별도 빌드나 단위 테스트는 사용하지 않습니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

중단 조건:

- 사용자 승인 없이 계약 경계나 공식 문서 의미를 바꿔야 하는 상황이 발견됩니다.
- 기존 미추적 또는 수정 파일과 충돌해 안전한 이동이 어렵습니다.
- `AGENTS.md` 수정 범위가 문서 구조 정합성을 넘어서는 동작 정책 변경으로 확대됩니다.

중단 처리:

- 진행 중인 체크리스트 항목을 `aborted`로 표시합니다.
- 이미 이동한 문서가 있다면 사용자에게 현재 상태와 선택지를 보고합니다.
- 사용자가 명시적으로 요청하지 않는 한 기존 변경을 파괴적으로 되돌리지 않습니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 답변에 따라 권장 섹션은 전체 고정하고, 문서에서 사용하지 않는 섹션은 `사용하지 않음`으로 명시하는 방향으로 결정했습니다.
- 2026-06-13: 루트 논의 문서 이동 시 파일명 시간은 실제 이동 시각을 사용하기로 결정했습니다.
- 2026-06-13: `closed` 논의 문서의 `Absorption Target (흡수 대상)`은 필수로 두기로 결정했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/open/`으로 이동하고 상태를 `open`으로 변경했습니다.
- 2026-06-13: 승인된 구조 개편을 완료하고 이 계획서를 `docs/plans/closed/`로 이동했습니다.

## Result (결과)

완료:

- 계약 문서를 `docs/contracts/`로 이동했습니다.
- `docs/architectures/`와 `docs/plans/` 구조를 추가했습니다.
- `.opencode-context/discussions/`를 상태 기반 구조로 갱신했습니다.
- 루트 논의 문서를 `.opencode-context/discussions/closed/`로 이동했습니다.
- `.opencode-context/decisions/`를 삭제하고 핵심 배경을 README에 흡수했습니다.
- `AGENTS.md`의 문서 구조 지침을 갱신하고 중복 `Graphify Policy`를 병합했습니다.
- `opencode.json`의 예전 `decision` command를 `discussion` command로 변경했습니다.

미완료 또는 중단 항목은 없습니다.

## References (근거 및 영향 문서)

근거:

- `docs-context-restructure-discussion.md`
- `.opencode-context/reports/008-docs-context-structure-consistency.md`
- `.opencode-context/reports/009-plan-discussion-section-policy.md`
- 삭제 전 `.opencode-context/decisions/001-opencode-context-directory.md`
- `docs/contracts/README.md`
- `.opencode-context/discussions/README.md`

영향:

- `AGENTS.md`
- `opencode.json`
- `docs/README.md`
- `docs/contracts/README.md`
- `docs/architectures/README.md`
- `docs/plans/README.md`
- `.opencode-context/README.md`
- `.opencode-context/discussions/README.md`
- `.opencode-context/reports/README.md`
- `.opencode-context/sessions/README.md`
- `.opencode-context/assets/README.md`
- 삭제된 `.opencode-context/decisions/`
- 이동된 `.opencode-context/contracts/`
