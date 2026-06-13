# Plan: context 디렉토리 이름 변경

## Status (상태)

archived

이 계획서는 모든 항목이 완료되어 보관된 계획서입니다.

## Summary (요약)

이 계획은 현재 `.opencode-context/`로 관리 중인 프로젝트 작업 맥락 디렉토리를 `.project-context/`로 변경합니다. 새 이름은 사용자가 확정했으며, 이전 경로 호환용 symlink나 안내 파일 없이 기존 경로를 완전히 제거하는 방향입니다.

과거 완료 문서의 본문은 역사적 설명을 보존하기 위해 일괄 치환하지 않습니다. 현재 정책과 실행 경로에 영향을 주는 파일만 새 경로로 갱신하고, 필요한 문서에는 현재 경로가 `.project-context/`임을 명시합니다.

## Goal (목표)

- 작업 맥락 디렉토리 이름을 의미상 더 정확한 `.project-context/`로 변경합니다.
- opencode 특정 도구명에 묶인 인상을 줄이고, 프로젝트 작업 맥락과 에이전트 협업 산출물 저장소라는 의미를 명확히 합니다.
- `AGENTS.md`, `opencode.json`, `.gitignore`, 현재 정책 README의 경로를 새 이름과 일치시킵니다.
- 이전 `.opencode-context/` 경로는 완전히 제거합니다.

## Scope (작업 범위)

포함:

- `.opencode-context/` 전체를 `.project-context/`로 이동합니다.
- `.project-context/README.md`의 정의를 새 이름에 맞게 갱신합니다.
- `AGENTS.md`의 현재 정책 경로를 `.project-context/`로 변경합니다.
- `opencode.json` command template의 checkpoint, handoff, discussion 경로를 `.project-context/`로 변경합니다.
- `.gitignore`의 inbox ignore/예외 규칙을 `.project-context/inbox/**` 기준으로 변경합니다.
- `.project-context/discussions/README.md`, reports/assets/sessions README의 현재 정책 경로를 점검하고 필요한 경우 갱신합니다.
- `docs/README.md`, `docs/plans/README.md` 등 현재 정책 문서 목록에서 새 경로가 필요한 부분을 갱신합니다.
- rename 논의 문서를 사용자 답변 기준으로 정리하고 `closed`로 이동합니다.
- 이 계획서를 승인 후 `doing`, 완료 후 `archived`로 이동합니다.

제외:

- 과거 완료 보고서, 완료 계획서, 닫힌 논의 문서 본문의 역사적 `.opencode-context` 언급은 일괄 치환하지 않습니다.
- 이전 `.opencode-context/` 경로에 symlink, 안내 파일, 호환 디렉토리를 남기지 않습니다.
- `docs/` 공식 문서 구조 자체는 변경하지 않습니다.
- opencode project config 위치는 변경하지 않습니다. 루트 `opencode.json`을 유지합니다.

## Non-Goals (제외 목표)

- 이 계획은 새 문서 체계를 다시 설계하지 않습니다.
- 이 계획은 reports, discussions, sessions, inbox, assets의 하위 구조를 바꾸지 않습니다.
- 이 계획은 과거 문서의 역사적 서술을 현재 경로로 재작성하지 않습니다.
- 이 계획은 opencode agent, skill, plugin의 기능을 변경하지 않습니다.

## Assumptions (가정)

- 새 이름은 `.project-context`로 확정되었습니다.
- 과거 완료 문서의 본문 경로는 설명 보존 원칙에 따라 유지합니다.
- 이전 `.opencode-context` 경로는 호환 레이어 없이 제거합니다.
- `.gitkeep` 정리 변경과 rename 논의 초안은 `f1ffa66 docs(context): preserve leaf directories`로 먼저 커밋되었습니다.
- 현재 실행 중인 opencode 세션은 설정 변경을 즉시 반영하지 않을 수 있으므로 완료 후 재시작 안내가 필요합니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_12-13-55_context-directory-rename.md`
- 선행 커밋: `f1ffa66 docs(context): preserve leaf directories`
- 관련 공식 구조: `docs/contracts`, `docs/architectures`, `docs/plans`
- 설정 파일: `opencode.json`
- 작업 지침: `AGENTS.md`

## Risks (리스크)

- 경로 변경 누락 시 command template 또는 지침이 존재하지 않는 디렉토리를 가리킬 수 있습니다.
- 과거 문서를 보존하기 때문에 검색 결과에는 `.opencode-context`가 계속 남습니다. 현재 정책 파일과 히스토리 문서를 구분해서 검증해야 합니다.
- `.gitignore` 경로 변경을 누락하면 `.project-context/inbox/`의 임시 입력 파일이 의도치 않게 추적될 수 있습니다.
- 현재 세션에서는 기존 시스템 지침이 남아 있을 수 있어 완료 후 opencode 재시작이 필요합니다.

## Plan Ground (계획 기반 체크리스트)

- [x] 승인 전 상태 확인
- [x] 디렉토리 rename
- [x] 현재 정책 파일 경로 갱신
- [x] 논의 문서 종료 처리
- [x] 계획 문서 상태 갱신
- [x] 검증

## Plan Tree (계획 트리)

- [x] 1. 승인 후 착수
- [x] 1.1. `git status` 확인
- [x] 1.2. 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경
- [x] 2. 디렉토리 이동
- [x] 2.1. `.opencode-context/`를 `.project-context/`로 이동
- [x] 2.2. 이전 `.opencode-context/` 경로가 남지 않았는지 확인
- [x] 3. 현재 정책 경로 갱신
- [x] 3.1. `.project-context/README.md` 갱신
- [x] 3.2. `AGENTS.md` 갱신
- [x] 3.3. `opencode.json` command template 갱신
- [x] 3.4. `.gitignore` inbox 규칙 갱신
- [x] 3.5. 현재 정책 README와 문서 목록 갱신
- [x] 4. 논의 문서 종료
- [x] 4.1. rename 논의 문서를 `draft`에서 `closed`로 이동
- [x] 4.2. 논의 문서의 `Status`, `Resolution`, `Absorption Target` 갱신
- [x] 5. 완료 처리
- [x] 5.1. 계획 체크리스트 갱신
- [x] 5.2. 계획서를 `docs/plans/archived/`로 이동
- [x] 6. 검증
- [x] 6.1. 현재 정책 파일에서 `.opencode-context` 잔여 경로 검색
- [x] 6.2. `opencode debug config` 실행
- [x] 6.3. `git status --short` 확인

## Checklist (전체 체크리스트)

- [x] CL-001: 승인 후 `git status` 확인 (done)
- [x] CL-002: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done)
- [x] CL-003: `.opencode-context/`를 `.project-context/`로 이동 (done)
- [x] CL-004: 이전 `.opencode-context/` 경로가 제거됐는지 확인 (done)
- [x] CL-005: `.project-context/README.md` 정의와 경로 갱신 (done)
- [x] CL-006: `AGENTS.md`의 작업 맥락 경로를 `.project-context/`로 갱신 (done)
- [x] CL-007: `opencode.json` command template 경로를 `.project-context/`로 갱신 (done)
- [x] CL-008: `.gitignore`의 inbox ignore/예외 규칙을 `.project-context/`로 갱신 (done)
- [x] CL-009: `.project-context/discussions/README.md` 문서 목록과 경로 확인 (done)
- [x] CL-010: `.project-context/reports/README.md`, sessions/assets/inbox README 경로 확인 (done)
- [x] CL-011: `docs/README.md`, `docs/plans/README.md` 등 현재 정책 문서 경로 갱신 (done)
- [x] CL-012: rename 논의 문서를 `closed`로 이동하고 `Status`를 `closed`로 갱신 (done)
- [x] CL-013: rename 논의 문서의 `Resolution`과 `Absorption Target` 갱신 (done)
- [x] CL-014: 현재 정책 파일에서 `.opencode-context` 잔여 경로 검색 (done)
- [x] CL-015: 과거 완료 문서의 역사적 `.opencode-context` 언급은 보존 대상인지 확인 (done)
- [x] CL-016: `opencode debug config` 실행 (done)
- [x] CL-017: 최종 `git status --short` 확인 (done)
- [x] CL-018: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done)

## Verification (검증)

검증 항목:

- `.opencode-context/` 디렉토리가 남아 있지 않은지 확인합니다.
- `.project-context/` 디렉토리가 기대한 하위 구조를 유지하는지 확인합니다.
- 현재 정책 파일에서 `.opencode-context` 경로가 남아 있지 않은지 확인합니다.
- 과거 완료 문서의 `.opencode-context` 언급은 히스토리 보존으로 남길 수 있음을 확인합니다.
- `opencode.json`이 새 경로를 사용하며 config 로딩에 실패하지 않는지 확인합니다.

검증 명령:

```sh
git status --short
opencode debug config
```

## Rollback Or Abort Plan (롤백 또는 중단 계획)

중단 조건:

- `.opencode-context/` 이동 중 예상하지 못한 파일 충돌이 발견됩니다.
- `.project-context/`로 바꿀 때 현재 정책 파일과 과거 히스토리 문서의 구분이 불명확해집니다.
- opencode config 검증이 실패하고 원인이 즉시 명확하지 않습니다.

중단 처리:

- 진행 중 체크리스트 항목을 `aborted`로 표시합니다.
- 이미 이동한 파일이 있다면 현재 상태를 보고하고 사용자 지시를 받습니다.
- 사용자 승인 없이 파괴적 reset이나 강제 되돌리기를 하지 않습니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자가 새 이름을 `.project-context`로 확정했습니다.
- 2026-06-13: 사용자가 과거 완료 문서 본문의 역사적 경로 설명은 보존하기로 결정했습니다.
- 2026-06-13: 사용자가 이전 `.opencode-context` 경로에 symlink나 안내 파일을 남기지 않고 완전히 제거하기로 결정했습니다.
- 2026-06-13: `.gitkeep` 정리 변경과 rename 논의 초안은 먼저 커밋했습니다.
- 2026-06-13: rename 논의 문서를 사용자 답변 기준으로 닫고, 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `.opencode-context/`를 `.project-context/`로 이동하고 현재 정책/설정 경로를 갱신했습니다.

## Result (결과)

완료:

- `.opencode-context/` 전체를 `.project-context/`로 이동했습니다.
- 이전 `.opencode-context/` 경로는 호환 레이어 없이 제거했습니다.
- `AGENTS.md`, `opencode.json`, `.gitignore`, 루트 README, `docs/README.md`, 현재 정책 README의 경로를 `.project-context/`로 갱신했습니다.
- 과거 완료 문서의 역사적 `.opencode-context` 본문 설명은 보존했습니다.

미완료 또는 중단 항목은 없습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_12-13-55_context-directory-rename.md`
- `f1ffa66 docs(context): preserve leaf directories`
- `7f9efd7 docs(context): reorganize documentation structure`

영향:

- `.opencode-context/`
- `.project-context/`
- `AGENTS.md`
- `opencode.json`
- `.gitignore`
- `docs/README.md`
- `docs/plans/README.md`
- `docs/plans/archived/2026-06-13_12-18-13_context-directory-rename.md`
