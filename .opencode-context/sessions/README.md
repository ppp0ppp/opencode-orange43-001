# Sessions (세션 체크포인트)

opencode 세션 중단, 작업 인계, 체크포인트를 Markdown으로 기록하는 위치입니다.

## Naming

세션 파일은 다음 형식을 사용합니다.

```text
YYYY-MM-DD_HH-MM-SS_short-slug.md
```

예시:

```text
2026-06-06_11-16-55_oh-my-opencode-slim-experiment.md
```

## Usage

- 새 세션이나 장기 작업 시작 시 가장 최근 세션 파일 1개를 먼저 확인합니다.
- 필요한 경우에만 과거 세션을 검색해서 읽습니다.
- 세션 파일은 대화 전문이 아니라 체크포인트와 goal 리스트로 사용합니다.
- 큰 작업 단위 종료, 하루 단위 종료, 재시작 전, 방향 전환 전후에 저장합니다.

## Template

```md
# Session Checkpoint (세션 체크포인트)

## Goal (목표)

이번 세션 또는 작업 단위의 목표를 적습니다.

## Current Status (현재 상태)

지금 어디까지 진행됐고, 무엇이 남았는지 적습니다.

## Completed (완료한 작업)

완료한 변경, 검증, 결정 사항을 적습니다.

## Next Steps (다음 단계)

다음 작업자가 바로 이어서 할 일을 적습니다.

## Open Questions (열린 질문)

사용자 확인이 필요하거나 아직 정하지 못한 질문을 적습니다.

## Important Files (중요 파일)

다음 작업자가 먼저 확인해야 할 파일 경로를 적습니다.

## Commands Run (실행한 명령)

중요한 검증, 빌드, 테스트 명령과 결과를 적습니다.

## Risks / Notes (리스크/메모)

주의해야 할 리스크, 미해결 이슈, 관련 discussion/decision 경로를 적습니다.
```
