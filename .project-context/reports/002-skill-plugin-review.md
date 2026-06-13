# Skill And Plugin Review

작성일: 2026-06-06

## 결론

현재 추가된 `git`, `git-worktree`, `tidy-tdd-first`, `graphify` skill은 템플릿의 기본 방향과 잘 맞습니다. 다만 Git Flow를 모든 프로젝트에 강제하는 것은 다소 강하므로, 장기적으로는 저장소별 정책 문서에서 branch 전략을 확인하도록 완화하는 편이 좋습니다.

`oh-my-opencode-slim`은 전체 설치보다 codemap, subtask, session goal, selected agents를 선별 흡수하는 방향이 적합합니다. `graphify`는 프로젝트 로컬 skill과 plugin을 설치했지만, 생성물은 커밋하지 않고 git hook/MCP/external backend는 별도 확인 후 활성화해야 합니다.

## Local Skills

### git

역할은 Conventional Commits와 브랜치/병합 흐름입니다. GitHub의 `git-commit` skill보다 범위가 넓어 사용자의 요구에 더 잘 맞습니다.

주의점은 Git Flow가 강하게 전제되어 있다는 점입니다. 모든 저장소가 `main`/`develop`/`feature`/`release`/`hotfix`를 쓰지는 않으므로, 실제 프로젝트에서는 `.opencode-context/contracts/` 또는 `.opencode/skills/git/REPOSITORIES.md`의 branch 전략을 우선 확인하도록 유지해야 합니다.

### git-worktree

worktree 기반 병렬 개발과 환경 분리에 유용합니다. `/tmp/worktrees`보다 `~/worktrees/<repo>/<branch-slug>`를 기본 선호 경로로 두는 편이 안전합니다.

worktree 제거, force remove, merge, prune은 사용자 확인을 거치는 것이 맞습니다.

### tidy-tdd-first

TDD와 Tidy First를 합친 skill로 적절합니다. 이름은 `tidy-tdd-first`로 정리했습니다.

초기 문서의 “항상 전체 테스트 실행”은 비용이 큰 저장소에서 부담이 되므로, 직접 관련 테스트를 우선 실행하고 완료 전 가능하면 더 넓은 테스트를 실행하는 방식으로 완화했습니다.

### graphify

프로젝트 로컬 graphify skill과 opencode plugin을 설치했습니다. plugin은 `graphify-out/graph.json`이 있을 때 bash 실행 전 graphify query 사용을 상기시키는 역할입니다.

`graphify-out/`은 로컬 산출물로 보고 커밋하지 않습니다. git hook과 MCP 서버는 기본 활성화하지 않았습니다.

## External Sources

### oh-my-opencode-slim

확인 URL: https://github.com/alvinunreal/oh-my-opencode-slim

확인된 특징은 다음입니다.

- OpenCode용 agent orchestration plugin
- orchestrator, explorer, oracle, council, librarian, designer, fixer 등 specialist agent 제공
- codemap, session management, session goal, subtask, MCP, websearch 관련 문서 제공
- 글로벌 설정 파일과 모델 preset을 생성하는 설치 흐름 제공

추천 도입 방식은 전체 설치보다 선별 흡수입니다. 특히 plugin이 설정과 agent routing을 크게 바꾸므로, 로컬 템플릿에서는 먼저 codemap/workflow 문서와 일부 agent prompt만 가져오는 것이 안전합니다.

### graphify

확인 URL: https://github.com/safishamsi/graphify

확인된 특징은 다음입니다.

- OpenCode 설치 지원
- `graphify-out/graph.html`, `GRAPH_REPORT.md`, `graph.json` 생성
- 코드 AST 추출은 로컬 처리
- 문서, PDF, 이미지 등은 backend에 따라 외부 LLM 호출 가능
- query log 기본 경로가 `~/.cache/graphify-queries.log`
- hook, MCP, PR 분석 기능 제공

현재는 프로젝트 로컬 skill과 opencode plugin까지 설치했습니다. hook 설치, MCP 등록, 외부 backend 사용은 별도 승인 후 진행해야 합니다.

### GitHub Skill

확인 URL: https://github.com/github/awesome-copilot/blob/main/skills/git-commit/SKILL.md

이 skill은 commit 생성에 집중되어 있습니다. 사용자가 원하는 브랜치 생성, 병합, worktree, PR 흐름까지 다루기에는 좁습니다.

현재 로컬 `git` skill이 더 넓은 요구를 충족하지만, GitHub issue/PR/check/release까지 다루는 별도 `github` skill은 추가할 가치가 있습니다.

## Recommendations

- `git` skill은 유지하되 Git Flow 강제 여부는 저장소별 문서로 조정합니다.
- `git-worktree` skill은 유지합니다.
- `tidy-tdd-first` skill은 유지합니다.
- `github` skill은 commit 전용이 아니라 issue, branch, PR, review, checks, release까지 포함하는 로컬 확장판으로 작성합니다.
- `graphify`는 설치 완료 상태이며, backend, hook, query log, 커밋 정책은 계속 보수적으로 관리합니다.
- `oh-my-opencode-slim`은 installer 실행보다 필요한 구성만 선별 흡수합니다.
