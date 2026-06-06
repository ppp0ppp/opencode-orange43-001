# Decisions (결정 기록)

중요한 설계 판단과 하네스 구성 결정을 ADR 또는 간단한 결정 기록으로 남기는 위치입니다.

## Naming (이름 규칙)

결정 기록은 다음 형식을 사용합니다.

```text
001-short-title.md
```

순번은 디렉토리 내에서 증가시키고, 제목은 짧은 kebab-case로 작성합니다.

## Usage (사용법)

- 이미 확정된 판단만 기록합니다.
- 뒤집힐 수 있는 논의 과정은 먼저 `../discussions/`에 기록합니다.
- 계약 경계면이 바뀌면 필요 시 `../contracts/`에도 반영합니다.

## Template (템플릿)

```md
# Decision (결정): short-title

## Status (상태)
Accepted | Superseded

현재 결정의 상태를 적습니다.

## Context (배경)

왜 이 결정이 필요했는지 적습니다.

## Decision (결정)

확정된 선택을 명확히 적습니다.

## Consequences (결과/영향)

이 결정으로 생기는 장점, 비용, 리스크를 적습니다.

## Related (관련 문서)

관련 discussion, report, contract 경로를 적습니다.
```
