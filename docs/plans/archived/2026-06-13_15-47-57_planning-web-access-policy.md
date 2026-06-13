# Plan: 논의/계획 단계 웹 접근 정책 반영

## Status (상태)

archived

## Summary (요약)

이 계획은 논의/계획 단계에서 필요한 경우 `webfetch`와 `websearch`를 사용할 수 있음을 루트 `README.md`에 명시하고, `opencode.json`에서 두 권한을 전역 `allow`로 변경합니다.

또한 웹 접근 결과를 계획서 `References`에 항상 기록하는 규칙을 `docs/plans/README.md`에 반영합니다. 비공식 출처는 사용자 승인 또는 별도 표시를 요구합니다.

## Goal (목표)

- 논의/계획 단계에서 공식 문서와 최신 외부 정보를 추측하지 않고 확인할 수 있게 합니다.
- `webfetch`와 `websearch`를 전역 허용합니다.
- 웹 접근 결과를 계획서 `References`에 일관되게 기록합니다.
- 비공식 출처 사용 시 사용자 승인 또는 별도 표시를 요구합니다.
- 민감정보를 웹 요청이나 검색 질의에 포함하지 않는 제약을 명시합니다.

## Scope (작업 범위)

포함:

- `opencode.json`의 `webfetch`, `websearch` 권한을 `allow`로 변경
- `README.md`에 `Web Access` 섹션 추가
- `docs/plans/README.md`에 웹 확인 결과의 `References` 기록 규칙 추가
- 계획서 상태 목록 갱신

제외:

- `AGENTS.md` 수정
- 웹 검색 provider, MCP, plugin 추가 구현
- 비공식 출처 자동 검증 도구 구현
- 기존 계획서 전체에 웹 References 소급 추가

## Non-Goals (제외 목표)

- 웹 검색 결과 자체를 공식 근거로 삼지 않습니다.
- 민감한 코드, 토큰, 개인정보, 내부 URL을 웹 요청에 포함하지 않습니다.
- `websearch` 도구가 노출되지 않는 환경에서 별도 검색 도구를 구현하지 않습니다.

## Assumptions (가정)

- 사용자는 `webfetch`와 `websearch` 전역 허용을 승인했습니다.
- 웹 접근 규칙은 루트 `README.md`에 반영합니다.
- 웹 접근 결과는 계획서 `References`에 항상 기록합니다.
- 비공식 출처는 사용자 승인 또는 별도 표시를 요구합니다.
- 현재 세션에서 `websearch` 도구가 노출되지 않을 수 있으며, 권한 허용과 도구 제공은 별개입니다.

## Dependencies (의존성)

- 근거 논의: `.project-context/discussions/closed/2026-06-13_15-42-07_planning-web-access-policy.md`
- 공식 schema: `https://opencode.ai/config.json`
- 공식 docs: `https://opencode.ai/docs`

## Risks (리스크)

- 전역 allow로 인해 에이전트가 웹 접근을 과도하게 사용할 수 있습니다.
- 검색 질의에 민감정보가 포함될 수 있습니다.
- 비공식 출처가 공식 기준처럼 사용될 수 있습니다.
- 웹 접근 결과를 공식 문서로 흡수하지 않으면 외부 정보 의존 드리프트가 생길 수 있습니다.

## Plan Ground (계획 기반 체크리스트)

- [x] 설정 변경
- [x] README 규칙 반영
- [x] plans README References 규칙 반영
- [x] 검증
- [x] 완료 처리

## Plan Tree (계획 트리)

```text
P1. 착수 처리
├─ P1.1. 계획서를 `doing`으로 이동
└─ P1.2. `docs/plans/README.md` 목록 갱신

P2. 웹 접근 정책 반영
├─ P2.1. `opencode.json`에서 `webfetch`와 `websearch`를 `allow`로 변경
├─ P2.2. `README.md`에 `Web Access` 섹션 추가
└─ P2.3. `docs/plans/README.md`에 웹 References 기록 규칙 추가

P3. 검증과 완료 처리
├─ P3.1. `opencode.json` JSON 문법 확인
├─ P3.2. 변경 문서와 상태 목록 확인
├─ P3.3. `git diff`로 변경 범위 확인
└─ P3.4. 계획서를 `archived`로 이동하고 결과 기록
```

## Checklist (전체 체크리스트)

- [x] CL-001: 계획서를 `docs/plans/doing/`으로 이동하고 `Status`를 `doing`으로 변경 (done, P: P1.1)
- [x] CL-002: `docs/plans/README.md` 문서 목록을 `scheduled`에서 `doing`으로 갱신 (done, P: P1.2)
- [x] CL-003: `opencode.json`에서 `webfetch`와 `websearch`를 `allow`로 변경 (done, P: P2.1)
- [x] CL-004: `README.md`에 논의/계획 단계 `Web Access` 섹션 추가 (done, P: P2.2)
- [x] CL-005: `docs/plans/README.md`에 웹 접근 결과 `References` 기록 규칙 추가 (done, P: P2.3)
- [x] CL-006: `opencode.json` JSON 문법 확인 (done, P: P3.1)
- [x] CL-007: 변경 문서와 상태 목록 확인 (done, P: P3.2)
- [x] CL-008: `git diff`로 변경 범위 확인 (done, P: P3.3)
- [x] CL-009: 계획서를 `docs/plans/archived/`로 이동하고 결과 기록 (done, P: P3.4)

## Verification (검증)

- `opencode.json`에서 `webfetch`와 `websearch`가 `allow`인지 확인합니다.
- `python3 -m json.tool opencode.json >/dev/null`로 JSON 문법을 확인합니다.
- `README.md`에 논의/계획 단계 웹 접근 규칙이 있는지 확인합니다.
- `docs/plans/README.md`에 웹 확인 결과를 `References`에 기록하는 규칙이 있는지 확인합니다.
- `.project-context/discussions/README.md`와 `docs/plans/README.md` 상태 목록이 맞는지 확인합니다.
- `git diff`로 의도한 파일만 변경됐는지 확인합니다.

## Rollback Or Abort Plan (롤백 또는 중단 계획)

- 웹 접근이 과도하다고 판단되면 `websearch`만 `ask`로 되돌리고 `webfetch`는 `allow`로 유지하는 절충안을 검토합니다.
- README가 과하게 길어지면 웹 접근 규칙을 더 짧게 줄이고 세부 규칙은 `docs/plans/README.md`로 이동합니다.

## Progress Notes (진행 메모)

- 2026-06-13: 사용자 승인에 따라 논의 문서를 닫고 이 계획서로 결론을 흡수했습니다.
- 2026-06-13: 사용자 승인 후 이 계획서를 `docs/plans/doing/`으로 이동하고 상태를 `doing`으로 변경했습니다.
- 2026-06-13: `opencode.json`, `README.md`, `docs/plans/README.md`에 웹 접근 정책을 반영했습니다.
- 2026-06-13: 검증 후 이 계획서를 `docs/plans/archived/`로 이동했습니다.

## Result (결과)

`opencode.json`에서 `webfetch`와 `websearch`를 전역 `allow`로 변경했습니다.

루트 `README.md`에는 논의/계획 단계의 웹 접근 정책을 추가했습니다. 공식 출처 우선, 민감정보 금지, 비공식 출처 승인/표시, 웹 접근 실패 시 보고 원칙을 명시했습니다.

`docs/plans/README.md`에는 계획 중 웹 접근을 사용했다면 `References`에 URL, 공식/비공식 여부, 확인 목적을 항상 기록하는 규칙과 예시를 추가했습니다.

## References (근거 및 영향 문서)

근거:

- `.project-context/discussions/closed/2026-06-13_15-42-07_planning-web-access-policy.md`
- 공식: `https://opencode.ai/config.json`: `webfetch`/`websearch` permission schema 확인
- 공식: `https://opencode.ai/docs`: opencode 공식 문서 위치 확인

영향:

- `opencode.json`
- `README.md`
- `docs/plans/README.md`
