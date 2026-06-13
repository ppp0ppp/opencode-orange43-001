# Plan: main/dev 브랜치 기반 템플릿 운영 전략 반영

## Status (상태)

doing

## Summary (요약)

이 계획은 `main`, `dev`, `feat/*` 브랜치 역할을 분리하는 템플릿 운영 전략을 공식 문서와 실제 브랜치 구성에 반영합니다.

`main`은 바로 클론해 사용할 수 있는 깨끗한 템플릿 브랜치로 유지하고, `dev`는 현재 문서와 생성 과정, 논의, 계획, 보고서, 세션 이력을 보존하는 개발 브랜치로 둡니다. 새 작업은 `feat/xxx`에서 만들고 `dev`에 병합하며, `main`에는 재사용 가능한 최종 산출물만 선별 반영합니다.

## Goal (목표)

- `main`을 즉시 사용 가능한 깨끗한 템플릿 브랜치로 정리합니다.
- `dev`에 현재 개발 이력과 구조 생성 과정을 보존합니다.
- 새 작업 흐름을 `feat/* -> dev -> main` 선별 반영으로 정리합니다.
- `main` README에 `dev` 브랜치에서 생성 과정을 확인할 수 있음을 명시합니다.
- `AGENTS.md`에 브랜치 작업 규칙을 짧게 반영합니다.

## Scope (작업 범위)

포함:

- `README.md`에 브랜치 정책 요약 추가
- `AGENTS.md`에 브랜치 작업 규칙 추가
- `dev` 브랜치 생성 또는 갱신
- `main`에서 실제 논의/보고서/세션/완료 계획 문서 제거
- `main`에 필요한 디렉토리 구조와 README 유지
- 빈 상태 디렉토리에 `.gitkeep` 추가
- `main`에 공용 `.opencode/` agents/skills/plugins 유지
- `main`에 graphify skill/plugin 유지, hook/MCP/외부 backend 기본 비활성 유지

제외:

- GitHub Actions 자동화
- release/tag 전략 상세 설계
- 다국어 README 작성
- 별도 release artifact 생성
- `dev` 전체를 `main`에 병합하는 작업

## Non-Goals (제외 목표)

- `main`에서 개발 이력 전체를 보존하지 않습니다.
- `main`에 실제 `.project-context/reports/`, `.project-context/sessions/`, `.project-context/discussions/closed/` 문서를 남기지 않습니다.
- `main`에 완료된 `docs/plans/archived/` 계획서를 남기지 않습니다.
- graphify hook, MCP 서버, 외부 backend를 기본 활성화하지 않습니다.

## Assumptions (가정)

- 현재 브랜치의 문서와 이력은 `dev`에서 보존해야 합니다.
- `main`은 새 사용자가 바로 클론하는 템플릿 진입점입니다.
- `main` 정리는 현재 변경을 잃지 않도록 `dev` 보존 이후 진행해야 합니다.
- `dev -> main` 반영은 초기에는 checkout path 방식으로 운용합니다.
- 브랜치 생성, 전환, 정리, 삭제는 사용자 승인 범위 안에서 수행합니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_14-35-20_branch-template-strategy.md`
- 관련 문서: `README.md`, `AGENTS.md`, `.project-context/README.md`, `docs/plans/README.md`

## Risks (리스크)

- `main` 정리 중 dev 보존이 누락되면 생성 과정과 운영 이력을 잃을 수 있습니다.
- `main`에서 너무 많은 문서를 제거하면 템플릿 사용자가 규칙을 이해하기 어려울 수 있습니다.
- `dev -> main` 선별 반영 기준이 흐려지면 브랜치 간 차이가 관리되지 않을 수 있습니다.
- `.opencode/` 공용 기능 중 일부가 외부 API나 hook을 암묵적으로 활성화하면 main 템플릿의 안전성이 떨어질 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [ ] 브랜치 상태 확인
- [ ] dev 보존 준비
- [ ] README/AGENTS 정책 반영
- [ ] main 템플릿 정리
- [ ] 검증
- [ ] 완료 처리

## Plan Tree (계획 트리)

```text
P1. 착수 처리
├─ P1.1. 계획서를 `doing`으로 이동
└─ P1.2. `docs/plans/README.md` 목록 갱신

P2. 브랜치 보존과 정책 반영 [now]
├─ P2.1. 현재 브랜치와 remote 상태 확인
├─ P2.2. `dev` 브랜치 생성 또는 갱신 전략 확정
├─ P2.3. `README.md`에 브랜치 정책 요약 추가
└─ P2.4. `AGENTS.md`에 `feat/* -> dev -> main` 작업 규칙 추가

P3. `main` 템플릿 정리
├─ P3.1. `main`에 유지할 파일 목록 확인
├─ P3.2. 실제 논의/보고서/세션/완료 계획 문서 제거
├─ P3.3. 필요한 빈 디렉토리에 `.gitkeep` 추가
└─ P3.4. 공용 `.opencode/` 기능과 README 유지 확인

P4. 검증과 완료 처리
├─ P4.1. `main` 파일 목록과 README 안내 확인
├─ P4.2. `dev` 보존 상태 확인
├─ P4.3. `git status`, `git diff`, 최근 커밋 확인
└─ P4.4. 계획서를 `archived`로 이동하고 결과 기록
```

## Checklist (전체 체크리스트)

- [x] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done, P: P1.1)
- [x] CL-002: `docs/plans/README.md` 문서 목록을 `scheduled`에서 `doing`으로 갱신 (done, P: P1.2)
- [x] CL-003: 현재 브랜치와 remote 상태를 확인 (done, P: P2.1)
- [ ] CL-004: `dev` 브랜치 생성 또는 갱신 전략을 확정하고 수행 (now doing, P: P2.2)
- [ ] CL-005: `README.md`에 브랜치 정책 요약을 추가 (pending, P: P2.3)
- [ ] CL-006: `AGENTS.md`에 브랜치 작업 규칙을 추가 (pending, P: P2.4)
- [ ] CL-007: `main`에 유지할 파일 목록을 확인 (pending, P: P3.1)
- [ ] CL-008: `main`에서 실제 논의/보고서/세션/완료 계획 문서를 제거 (pending, P: P3.2)
- [ ] CL-009: 필요한 빈 디렉토리에 `.gitkeep`을 추가 (pending, P: P3.3)
- [ ] CL-010: 공용 `.opencode/` 기능과 README 유지 여부를 확인 (pending, P: P3.4)
- [ ] CL-011: `main` 파일 목록과 README 안내를 확인 (pending, P: P4.1)
- [ ] CL-012: `dev` 보존 상태를 확인 (pending, P: P4.2)
- [ ] CL-013: `git status`, `git diff`, 최근 커밋을 확인 (pending, P: P4.3)
- [ ] CL-014: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (pending, P: P4.4)

## Verification (검증)

- `main` README에 `dev` 브랜치에서 생성 과정과 이력을 확인할 수 있다는 안내가 있는지 확인합니다.
- `AGENTS.md`에 `feat/* -> dev -> main` 선별 반영 규칙이 있는지 확인합니다.
- `main`에 실제 논의, 보고서, 세션, 완료 계획 문서가 남아 있지 않은지 확인합니다.
- `main`에 필요한 디렉토리 구조가 README 또는 `.gitkeep`로 유지되는지 확인합니다.
- `dev`가 현재 이력 보존 브랜치로 존재하는지 확인합니다.
- graphify skill/plugin은 유지하되 hook/MCP/외부 backend가 기본 활성화되지 않았는지 확인합니다.
- `git status`, `git diff`, 최근 커밋을 확인합니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

- `dev` 보존이 확인되지 않으면 `main` 정리를 시작하지 않습니다.
- `main` 정리 중 필요한 템플릿 문서가 과도하게 제거됐다고 판단되면 정리를 중단하고 유지 목록을 재검토합니다.
- 브랜치 전환이나 병합 중 충돌이 발생하면 즉시 중단하고 사용자에게 상태를 보고합니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 승인에 따라 논의 문서를 닫고 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 현재 브랜치가 `main`이고 local branch는 `main`만 있으며 remote는 `origin`임을 확인했습니다.
- 2026-06-13: 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.

## Result (결과)

현재 없음

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_14-35-20_branch-template-strategy.md`

영향:

- `README.md`
- `AGENTS.md`
- `main` 브랜치
- `dev` 브랜치
- `feat/*` 브랜치 운영 규칙
