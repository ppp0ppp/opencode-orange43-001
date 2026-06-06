# Discussions (논의)

아키텍처, 기술 스택, 개발 철학, 운영 방식처럼 결정 전 협의 과정이 자주 바뀌는 내용을 기록하는 위치입니다.

## Naming

논의 파일은 다음 형식을 사용합니다.

```text
YYYY-MM-DD_HH-MM-SS_short-slug.md
```

예시:

```text
2026-06-06_14-30-00_backend-runtime-strategy.md
```

## Usage

- 결정 전 사고 과정, 후보안, 질문, 반대 의견, 트레이드오프를 남깁니다.
- 확정된 결론은 필요 시 `../decisions/`의 ADR 또는 결정 기록으로 승격합니다.
- 세션 체크포인트에는 필요한 경우에만 관련 discussion 경로와 현재 결론을 짧게 기록합니다.
- 목표, 계약 경계, 기술 선택, 운영 영향, 보안/비용/성능 리스크가 불명확하면 작업자는 사용자에게 질문합니다.

## Template

```md
# Architecture Discussion (아키텍처 논의): short-title

## Status (상태)
Draft | In Discussion | Decided | Superseded

현재 상태를 하나만 남깁니다. 초안이면 Draft, 논의 중이면 In Discussion, 확정되면 Decided, 대체되면 Superseded를 사용합니다.

## Goal (목표)

이 논의로 무엇을 정하려는지 적습니다.

## Context (배경)

왜 지금 이 논의가 필요한지 적습니다.

## Scope (범위)

포함되는 범위와 제외되는 범위를 적습니다.

## Environment (환경)

개발, 테스트, 배포, 운영 환경과 관련 조건을 적습니다.

## Stack (언어/버전/프레임워크)

언어, 런타임 버전, 프레임워크, 주요 라이브러리를 적습니다.

## Philosophy (개발 사상/철학)

이 선택에서 우선할 가치와 코딩/운영 원칙을 적습니다.

## Constraints (제약)

기술적, 비즈니스적, 운영적 제약을 적습니다.

## Options (대안)

후보안을 A/B/C처럼 나누어 적습니다.

## Trade-offs (트레이드오프)

각 대안의 장점, 단점, 리스크를 적습니다.

## Questions (질문)

작업자가 추측하면 안 되고 사용자 확인이 필요한 질문을 적습니다.

## Current Leaning (현재 선호안)

아직 확정이 아니라면 현재 선호안과 이유를 적습니다.

## Decision (결정)

확정된 경우에만 결론을 적습니다. 미정이면 비워두거나 `미정`으로 둡니다.

## Impact (영향)

영향받는 파일, 모듈, API, DB, 운영 방식, 비용을 적습니다.

## Verification (검증 계획)

결정이 맞는지 확인할 테스트, 실험, 리뷰 방법을 적습니다.

## Follow-ups (후속 작업)

다음 논의, 구현 작업, 문서화 항목을 적습니다.
```
