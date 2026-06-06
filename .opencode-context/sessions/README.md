# Sessions

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
# Session Checkpoint

## Goal

## Current Status

## Completed

## Next Steps

## Open Questions

## Important Files

## Commands Run

## Risks / Notes
```
