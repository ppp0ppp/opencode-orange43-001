# Project Setup (프로젝트 설정)

이 파일은 사용자가 프로젝트 시작 전에 목표, 환경, 기술 선택, 개발 철학을 미리 적어 작업자에게 전달하기 위한 입력 문서입니다.

`AGENTS.md`는 작업자 행동 규칙이고, `PROJECT.md`는 이 프로젝트 자체의 맥락과 선호를 담습니다. 불확실한 항목은 비워두거나 `미정`으로 표시해도 됩니다.

## Goal (목표)

이 프로젝트가 달성해야 하는 최종 목표와 성공 기준을 적습니다.

예: 내부 운영 도구 MVP를 만들고, 관리자 3명이 실제 업무에 사용할 수 있으면 성공으로 봅니다.

## Scope (범위)

포함할 것과 제외할 것을 구분합니다.

예: 사용자 관리와 감사 로그는 포함하고, 결제 기능은 제외합니다.

## Environment (환경)

개발, 테스트, 배포, 운영 환경을 적습니다.

예: 로컬 Linux, Docker Compose, 단일 VPS 배포, PostgreSQL managed DB.

## Environment Setup (환경 설정)

프로젝트를 실행하기 위해 준비해야 하는 환경을 3단계로 나누어 적습니다.

### Target OS Runners (타겟 OS 실행자)

OS별 shell, Git, 패키지 매니저, Docker, 언어 버전 관리자, PATH 설정을 적습니다.

### opencode Tool Runners (opencode 도구 실행자)

opencode, 로컬 skill/plugin/hook/MCP/agent 사용에 필요한 CLI와 버전을 적습니다.

예: opencode CLI, Git, graphify CLI, graphify 설치용 Python 3.10 이상과 `uv` 또는 `pipx`.

### Development Target (개발 타겟)

실제 앱을 실행하고 테스트하기 위한 언어, 프레임워크, DB, 외부 서비스, 여러 앱의 실행 순서를 적습니다.

예: backend는 Python/FastAPI, frontend는 Vite/TypeScript, worker는 LangGraph, DB는 PostgreSQL.

## Stack (언어/버전/프레임워크)

언어, 런타임 버전, 프레임워크, 주요 라이브러리, 패키지 매니저를 적습니다.

예: Python 3.12, FastAPI, PostgreSQL 16, 패키지 매니저 미정.

## Philosophy (개발 사상/철학)

프로젝트에서 우선할 개발 기준을 적습니다.

예: 작은 변경, 명시적 코드, 운영 단순성, 테스트 가능한 구조를 우선합니다.

## Constraints (제약)

기술적, 비즈니스적, 운영적 제약을 적습니다.

예: 월 비용 20달러 이하, 외부 SaaS 최소화, 개인정보 외부 전송 금지.

## Contract Boundaries (계약 경계)

API, DB, 이벤트, public interface, 인증/권한, 모듈 경계처럼 변경 전 확인이 필요한 경계를 적습니다.

예: 공개 REST API와 DB schema 변경은 사용자 확인 후 진행합니다.

## Quality Bar (품질 기준)

테스트, lint, 타입 검사, 성능, 보안, 접근성 등 완료 기준을 적습니다.

예: 핵심 로직은 테스트를 추가하고, 변경 범위의 기존 테스트는 통과해야 합니다.

## Open Questions (열린 질문)

아직 정하지 못했거나 작업자가 반드시 확인해야 하는 질문을 적습니다.

예: 배포 대상 클라우드를 AWS로 할지, 단일 VPS로 시작할지 미정입니다.
