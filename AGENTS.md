# Project Assistant Defaults

이 파일은 이 프로젝트를 opencode 기본 설정 템플릿으로 사용할 때 적용할 공통 지시문입니다.

## Communication

- 기본 응답 언어는 한국어로 합니다. 사용자가 다른 언어를 쓰면 그 언어를 따릅니다.
- 결론을 먼저 말하고, 필요한 세부사항만 간결하게 덧붙입니다.
- 불확실한 요구사항은 추측하지 말고 짧게 확인합니다.
- 코드 리뷰 요청에서는 문제점과 리스크를 먼저 제시하고, 요약은 뒤에 둡니다.

## Engineering Defaults

- 변경 전 코드베이스를 먼저 확인하고, 가장 작은 올바른 변경을 선호합니다.
- 기존 스타일, 구조, 네이밍을 우선 유지합니다.
- 불필요한 추상화, 호환성 레이어, 새 헬퍼를 만들지 않습니다.
- 사용자가 명시하지 않은 기존 변경사항은 되돌리거나 덮어쓰지 않습니다.
- 파괴적 명령, 강제 푸시, 커밋 수정은 명시적 요청 없이는 하지 않습니다.

## Context Files

- 프로젝트별 목표, 환경, 스택, 개발 철학, 제약은 가능하면 루트 `PROJECT.md`에 사용자가 미리 기록합니다.
- 새 프로젝트 세팅이나 장기 작업을 시작할 때 `PROJECT.md`가 있으면 먼저 확인하고, 비어 있거나 모호한 필수 항목은 사용자에게 질문합니다.
- opencode와 사용자가 큰 맥락을 Markdown으로 주고받을 때는 `.opencode-context/`를 기준 디렉토리로 사용합니다.
- 보고서는 `.opencode-context/reports/`, 논의 과정은 `.opencode-context/discussions/`, 의사결정 기록은 `.opencode-context/decisions/`, 세션 체크포인트는 `.opencode-context/sessions/`, 계약/스키마 문서는 `.opencode-context/contracts/`에 둡니다.
- 보고서, 의사결정, 계약 문서는 `001-short-title.md`처럼 3자리 순번과 짧은 kebab-case 제목을 사용합니다.
- 논의 파일과 세션 체크포인트는 `.opencode-context/discussions/YYYY-MM-DD_HH-MM-SS_short-slug.md`, `.opencode-context/sessions/YYYY-MM-DD_HH-MM-SS_short-slug.md` 형식을 사용합니다.
- 새 세션이나 장기 작업을 시작할 때는 가장 최근 세션 파일 1개를 먼저 확인하고, 필요한 경우에만 과거 세션을 검색해서 읽습니다.
- 세션 파일은 대화 전문이 아니라 goal, 상태, 완료 작업, 다음 단계, 열린 질문, 중요 파일, 실행 명령 중심으로 짧게 유지합니다.
- 중요한 설계 판단, 하루 단위 작업 종료, 큰 작업 단위 종료, 중단 전 상태, 다음 작업 인계가 필요하면 Markdown 체크포인트를 남깁니다.

## Architecture Discussions

- 아키텍처, 기술 스택, 개발 철학, 운영 방식처럼 뒤집힐 수 있는 협의 과정은 `.opencode-context/discussions/`에 기록합니다.
- discussions는 결정 전 사고 과정, 후보안, 질문, 트레이드오프, 현재 선호안을 담습니다.
- 확정된 결정은 필요 시 `.opencode-context/decisions/`로 승격해 별도 기록합니다.
- sessions에는 discussion 전문을 올리지 않고, 필요한 경우 관련 파일 경로와 현재 결론만 짧게 기록합니다.
- 논의에는 목표, 배경, 범위, 환경, 언어/버전/프레임워크, 개발 사상, 제약, 대안, 리스크, 검증 계획을 가능한 한 명시합니다.
- 목표, 성공 기준, 계약 경계, 기술 선택, 운영 영향, 보안/비용/성능 리스크가 불명확하면 작업자는 추측하지 말고 사용자에게 질문합니다.

## Environment Setup

- 환경 설정은 타겟 OS 실행자, opencode 도구 실행 환경, 개발 타겟 환경으로 구분합니다.
- opencode 도구 실행 환경은 `opencode.json`, `.opencode/skills/`, `.opencode/plugins/`, `.opencode/agents/`, hook, MCP 서버가 실제로 요구하는 CLI와 버전을 기준으로 확인합니다.
- 개발 타겟 환경은 루트 `PROJECT.md`를 기준으로 확인하고, 언어/프레임워크/DB/복합 앱 구조가 미정이면 `.opencode-context/discussions/`에 먼저 논의합니다.
- 이 템플릿의 Python/`uv` 사용은 opencode 보조 도구 설치나 템플릿 유지보수 목적일 수 있으므로, 사용자 확인 없이 개발 타겟의 필수 런타임으로 간주하지 않습니다.

## Contract Boundaries

- API 스키마, DB 스키마, 이벤트 포맷, public interface, 모듈 경계, 인증/권한 경계는 계약 경계면으로 간주합니다.
- 계약 경계면을 추가, 삭제, 이름 변경, 의미 변경, 호환성 변경하려면 수정 전에 사용자에게 확인합니다.
- 계약 변경 제안에는 변경 이유, 영향 범위, 대안, 마이그레이션 필요 여부, 검증 계획을 포함합니다.
- 사용자의 명시 승인 없이 임시 호환성 레이어, 필드 추가/삭제, 경계 우회, 대규모 리팩터링을 하지 않습니다.
- 계약 문서가 `.opencode-context/contracts/`에 있으면 그 내용을 우선 기준으로 삼습니다.

## Git And Worktrees

- git 작업 전에는 `git status`, 필요한 경우 `git diff`, 최근 커밋 맥락을 확인합니다.
- 병렬 개발, 실험, 대규모 변경, 브랜치별 격리가 필요하면 git worktree 사용을 제안합니다.
- worktree는 가능하면 `~/worktrees/<repo>/<branch-slug>`처럼 재부팅 후에도 유지되는 위치를 선호합니다.
- worktree 제거 전에는 변경사항 커밋/보존 여부와 merge 여부를 확인합니다.
- 브랜치 생성, 병합, rebase, push, tag, worktree 삭제는 사용자 의도를 확인한 뒤 수행합니다.

## Tool Selection

- 빠른 위치 탐색과 텍스트 검색은 Glob/Grep을 우선 사용합니다.
- LSP는 심볼 정의, 참조, 타입/진단처럼 언어 서버가 강한 질문에 사용합니다.
- codemap은 명시적으로 사람이 읽는 폴더별 요약 지도가 필요할 때만 사용합니다.
- graphify는 대규모 구조 이해, 장기 프로젝트 맥락, 브랜치/PR 간 영향 분석, 코드와 문서의 관계 탐색에 사용합니다.
- graphify, codemap, LSP가 겹치면 작은 질문은 Grep/LSP, 장기/대규모 관계 질문은 graphify, 문서화 목적의 폴더별 지도는 codemap을 우선합니다.

## Graphify Policy

- graphify 도입 전에는 설치 방식, 생성 파일, hook, 외부 API 사용, query log 경로를 확인합니다.
- 이 템플릿은 프로젝트 로컬 graphify skill과 opencode plugin을 포함하지만, git hook과 MCP 서버는 기본 활성화하지 않습니다.
- graphify 생성물은 기본적으로 `graphify-out/`에 두며 커밋하지 않습니다.
- 브랜치 생성/병합, 대규모 리팩터링, 계약 경계면 변경, 주요 의존성 변경 후에는 graphify update 또는 재생성을 제안합니다.
- graphify hook 설치, MCP 서버 등록, 외부 backend 사용은 사용자 확인 후 수행합니다.
- 민감한 코드나 문서가 포함된 저장소에서는 graphify의 backend와 외부 전송 여부를 먼저 확인합니다.

## Plugin Policy

- opencode plugin은 실행 훅으로 도구 호출과 설정에 영향을 줄 수 있으므로 기본적으로 보수적으로 도입합니다.
- 새 플러그인은 출처, 라이선스, 유지보수 상태, 권한 범위, 네트워크 사용, 생성 파일을 확인한 뒤 추가합니다.
- 플러그인은 가능하면 프로젝트 로컬에 먼저 설치하거나 별도 브랜치/worktree에서 검증합니다.
- 자동 실행 hook, git hook, 외부 API 호출, 파일 대량 생성 기능은 사용자 확인 없이 활성화하지 않습니다.
- `oh-my-opencode-slim`은 전체 복사보다 필요한 agent, skill, command, codemap workflow를 선별 흡수하는 방향을 우선합니다.

## Slim Absorption Policy

- `oh-my-opencode-slim` 전체 plugin, TUI 설정, model preset, MCP 서버, `.slim` 상태 디렉토리는 기본 활성화하지 않습니다.
- plugin 의존성이 없는 skill이나 prompt는 project-local 파일로 작게 흡수합니다.
- slim 계열 read-only advisor는 구현을 맡기지 않고 리뷰, 아키텍처 판단, 단순화 검토에 한정합니다.
- codemap script와 `.slim/codemap.json`은 graphify 정책과 충돌할 수 있으므로 명시적 요청 전에는 도입하지 않습니다.

## Verification

- 가능한 경우 변경과 직접 관련된 테스트나 빌드만 실행합니다.
- 검증을 실행하지 못했거나 생략했다면 이유를 명확히 말합니다.
- 최종 응답에는 변경 파일과 검증 결과를 짧게 포함합니다.

## Graphify Policy

이 프로젝트는 `graphify-out/`의 로컬 graphify knowledge graph를 사용할 수 있습니다. graph에는 god node, community structure, 파일 간 관계가 포함될 수 있습니다.

사용자가 `/graphify`를 입력하면 다른 작업보다 먼저 `skill` 도구를 `skill: "graphify"`로 호출합니다.

규칙:
- 코드베이스 질문에서는 `graphify-out/graph.json`이 있으면 먼저 `graphify query "<question>"`를 실행합니다. 관계 확인에는 `graphify path "<A>" "<B>"`, 특정 개념 확인에는 `graphify explain "<concept>"`를 사용합니다. 이 명령들은 보통 `GRAPH_REPORT.md`나 raw grep 결과보다 작은 scoped subgraph를 반환합니다.
- hook이나 incremental update 뒤에는 `graphify-out/` 파일이 dirty 상태일 수 있습니다. dirty graph 파일만으로 graphify 사용을 건너뛰지 않습니다. stale/incorrect graph output 자체가 작업 대상이거나 사용자가 명시적으로 사용하지 말라고 한 경우에만 건너뜁니다.
- `graphify-out/wiki/index.md`가 있으면 넓은 탐색에는 raw source browsing보다 이 파일을 먼저 사용합니다.
- `graphify-out/GRAPH_REPORT.md`는 넓은 아키텍처 리뷰가 필요하거나 query/path/explain 결과만으로 맥락이 부족할 때만 읽습니다.
- 코드 수정 후 `graphify-out/graph.json`이 있으면 graph를 최신 상태로 유지하기 위해 `graphify update .`를 실행합니다. 이 업데이트는 AST-only이며 API 비용이 없습니다.
