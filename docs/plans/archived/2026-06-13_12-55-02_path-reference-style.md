# Plan: 문서 경로 표기 방식 표준화

## Status (상태)

archived

이 계획서는 모든 항목이 완료되어 보관된 계획서입니다.

## Summary (요약)

이 계획은 프로젝트 문서의 경로 표기를 프로젝트 루트 기준 경로로 강제하는 표준을 반영합니다.

최종 정책은 `docs/...`, `.project-context/...`, `AGENTS.md`, `opencode.json`처럼 프로젝트 루트에서 시작하는 경로를 모든 문서 본문과 문서 목록에 사용하는 것입니다. 문서 위치 기준 상대 경로와 Markdown 클릭 링크 병기는 기본적으로 사용하지 않습니다.

## Goal (목표)

- 경로 표기 기본값을 프로젝트 루트 기준 경로로 통일합니다.
- README 문서 목록에서도 짧은 상대 경로를 제거합니다.
- `AGENTS.md`에 향후 문서 작성 규칙을 명시합니다.
- 계획서, 논의 문서, 보고서가 상태 디렉토리 이동 후에도 안정적인 경로 표기를 유지하게 합니다.

## Scope (작업 범위)

포함:

- `AGENTS.md`에 프로젝트 루트 기준 경로 표기 규칙을 추가합니다.
- `docs/plans/README.md`의 문서 목록을 프로젝트 루트 기준 경로로 변경합니다.
- `.project-context/discussions/README.md`의 문서 목록을 프로젝트 루트 기준 경로로 변경합니다.
- 현재 진행 중인 이 계획서와 닫힌 논의 문서의 주요 참조 경로를 프로젝트 루트 기준으로 유지합니다.
- 경로 표기 논의 문서를 `closed` 상태로 유지하고 결론을 계획서와 연결합니다.

제외:

- 과거 완료 문서 본문 전체를 일괄 치환하지 않습니다.
- Markdown 클릭 링크를 추가하지 않습니다.
- 문서 링크 검사 도구나 자동화는 도입하지 않습니다.
- `docs/` 또는 `.project-context/` 디렉토리 구조는 변경하지 않습니다.

## Non-Goals (제외 목표)

- 이 계획은 문서 구조를 다시 설계하지 않습니다.
- 이 계획은 과거 역사적 설명의 경로를 현재 정책에 맞춰 재작성하지 않습니다.
- 이 계획은 GitHub에서 클릭 가능한 링크 UX를 최적화하지 않습니다.

## Assumptions (가정)

- 사용자는 프로젝트 루트 기준 경로 표기를 표준으로 승인했습니다.
- 사용자는 README 문서 목록의 짧은 상대 경로를 허용하지 않기로 결정했습니다.
- 사용자는 Markdown 클릭 링크 병기가 필요하지 않다고 결정했습니다.
- 표준 규칙은 우선 `AGENTS.md`에 명시합니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_12-49-18_path-reference-style.md`
- 관련 계획: `docs/plans/archived/2026-06-13_12-18-13_context-directory-rename.md`
- 영향 문서: `AGENTS.md`, `docs/plans/README.md`, `.project-context/discussions/README.md`

## Risks (리스크)

- 루트 기준 경로는 Markdown 렌더러에서 자동 클릭 링크가 되지 않을 수 있습니다.
- 과거 완료 문서 본문은 보존하므로 검색 결과에는 짧은 상대 경로나 과거 경로가 일부 남을 수 있습니다.
- README 문서 목록까지 루트 기준으로 쓰면 목록이 길어질 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] 승인 전 상태 확인
- [x] `AGENTS.md` 경로 표기 규칙 추가
- [x] README 문서 목록 경로 표준화
- [x] 계획서 상태 갱신
- [x] 검증

## Plan Tree (계획 트리)

- [x] 1. 승인 후 착수
- [x] 1.1. `git status` 확인
- [x] 1.2. 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경
- [x] 2. 규칙 명시
- [x] 2.1. `AGENTS.md`에 프로젝트 루트 기준 경로 표기 규칙 추가
- [x] 3. 문서 목록 표준화
- [x] 3.1. `docs/plans/README.md` 문서 목록을 루트 기준 경로로 변경
- [x] 3.2. `.project-context/discussions/README.md` 문서 목록을 루트 기준 경로로 변경
- [x] 4. 완료 처리
- [x] 4.1. 체크리스트 완료 처리
- [x] 4.2. 계획서를 `docs/plans/archived/`로 이동
- [x] 5. 검증
- [x] 5.1. 현재 정책 문서에서 짧은 상대 문서 목록 잔여 확인
- [x] 5.2. `git status --short` 확인

## Checklist (전체 체크리스트)

- [x] CL-001: 승인 후 `git status` 확인 (done)
- [x] CL-002: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done)
- [x] CL-003: `AGENTS.md`에 프로젝트 루트 기준 경로 표기 규칙 추가 (done)
- [x] CL-004: `docs/plans/README.md` 문서 목록을 루트 기준 경로로 변경 (done)
- [x] CL-005: `.project-context/discussions/README.md` 문서 목록을 루트 기준 경로로 변경 (done)
- [x] CL-006: 현재 정책 문서에서 짧은 상대 문서 목록 잔여 확인 (done)
- [x] CL-007: 최종 `git status --short` 확인 (done)
- [x] CL-008: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done)

## Verification (검증)

검증 항목:

- `AGENTS.md`에 경로 표기 규칙이 명시되어 있는지 확인합니다.
- `docs/plans/README.md`의 문서 목록이 `docs/plans/...`로 시작하는지 확인합니다.
- `.project-context/discussions/README.md`의 문서 목록이 `.project-context/discussions/...`로 시작하는지 확인합니다.
- 불필요한 Markdown 클릭 링크가 추가되지 않았는지 확인합니다.

검증 명령:

```sh
git status --short
```

## Rollback Or Abort Plan (롤백 또는 중단 계획)

중단 조건:

- 루트 기준 경로 강제 규칙이 기존 README 문서 목록과 충돌해 사용성이 크게 떨어지는 경우
- 과거 완료 문서까지 대규모로 수정해야 하는 상황이 발견되는 경우

중단 처리:

- 진행 중 체크리스트 항목을 `aborted`로 표시합니다.
- 변경 범위와 미해결 쟁점을 사용자에게 보고합니다.
- 사용자 승인 없이 과거 완료 문서를 대규모 치환하지 않습니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자가 프로젝트 루트 기준 경로 표기를 표준으로 승인했습니다.
- 2026-06-13: 사용자가 README 문서 목록의 짧은 상대 경로도 허용하지 않기로 결정했습니다.
- 2026-06-13: 사용자가 Markdown 클릭 링크 병기는 필요하지 않다고 결정했습니다.
- 2026-06-13: 사용자가 규칙은 우선 `AGENTS.md`에 명시하면 된다고 판단했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `AGENTS.md`에 루트 기준 경로 표기 규칙을 추가하고 README 문서 목록을 루트 기준으로 정리했습니다.

## Result (결과)

완료:

- `AGENTS.md`에 프로젝트 루트 기준 경로 표기 규칙을 추가했습니다.
- `docs/plans/README.md` 문서 목록을 루트 기준 경로로 변경했습니다.
- `.project-context/discussions/README.md` 문서 목록을 루트 기준 경로로 변경했습니다.

미완료 또는 중단 항목은 없습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_12-49-18_path-reference-style.md`
- `docs/plans/archived/2026-06-13_12-18-13_context-directory-rename.md`

영향:

- `AGENTS.md`
- `docs/plans/README.md`
- `.project-context/discussions/README.md`
- `docs/plans/archived/2026-06-13_12-55-02_path-reference-style.md`
