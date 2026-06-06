# Discussions

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
# Architecture Discussion: short-title

## Status
Draft | In Discussion | Decided | Superseded

## Goal

## Context

## Scope

## Environment

## Stack

## Philosophy

## Constraints

## Options

## Trade-offs

## Questions

## Current Leaning

## Decision

## Impact

## Verification

## Follow-ups
```
