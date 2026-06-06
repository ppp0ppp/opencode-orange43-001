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

- opencode와 사용자가 큰 맥락을 Markdown으로 주고받을 때는 `.opencode-context/`를 기준 디렉토리로 사용합니다.
- 보고서는 `.opencode-context/reports/`, 의사결정 기록은 `.opencode-context/decisions/`, 세션 체크포인트는 `.opencode-context/sessions/`, 계약/스키마 문서는 `.opencode-context/contracts/`에 둡니다.
- 보고서, 의사결정, 계약 문서는 `001-short-title.md`처럼 3자리 순번과 짧은 kebab-case 제목을 사용합니다.
- 세션 체크포인트는 `.opencode-context/sessions/YYYY-MM-DD_HH-MM-SS_short-slug.md` 형식을 사용합니다.
- 새 세션이나 장기 작업을 시작할 때는 가장 최근 세션 파일 1개를 먼저 확인하고, 필요한 경우에만 과거 세션을 검색해서 읽습니다.
- 세션 파일은 대화 전문이 아니라 goal, 상태, 완료 작업, 다음 단계, 열린 질문, 중요 파일, 실행 명령 중심으로 짧게 유지합니다.
- 중요한 설계 판단, 하루 단위 작업 종료, 큰 작업 단위 종료, 중단 전 상태, 다음 작업 인계가 필요하면 Markdown 체크포인트를 남깁니다.

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

## graphify

This project can use a local graphify knowledge graph at graphify-out/ with god nodes, community structure, and cross-file relationships.

When the user types `/graphify`, invoke the `skill` tool with `skill: "graphify"` before doing anything else.

Rules:
- For codebase questions, first run `graphify query "<question>"` when graphify-out/graph.json exists. Use `graphify path "<A>" "<B>"` for relationships and `graphify explain "<concept>"` for focused concepts. These return a scoped subgraph, usually much smaller than GRAPH_REPORT.md or raw grep output.
- Dirty graphify-out/ files are expected after hooks or incremental updates; dirty graph files are not a reason to skip graphify. Only skip graphify if the task is about stale or incorrect graph output, or the user explicitly says not to use it.
- If graphify-out/wiki/index.md exists, use it for broad navigation instead of raw source browsing.
- Read graphify-out/GRAPH_REPORT.md only for broad architecture review or when query/path/explain do not surface enough context.
- After modifying code, run `graphify update .` when graphify-out/graph.json exists to keep the graph current (AST-only, no API cost).
