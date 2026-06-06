# Session Checkpoint

작성일: 2026-06-06

## Goal

다음 세션에서 `oh-my-opencode-slim`을 실험합니다. 우선순위는 `.opencode-context/reports/004-oh-my-opencode-slim-adoption.md`의 “선별 흡수 우선순위”를 따릅니다.

## Current Status

- opencode 기본 설정 템플릿의 첫 커밋이 생성되었습니다.
- 최신 커밋은 `5cf7772 chore: initialize opencode defaults template`입니다.
- graphify CLI는 설치되어 있으며 확인된 버전은 `0.8.32`입니다.
- 프로젝트 로컬 graphify skill과 opencode plugin은 설치되어 있습니다.
- graphify git hook과 MCP 서버는 활성화하지 않았습니다.
- `graphify-out/`은 `.gitignore`에 포함되어 커밋하지 않는 정책입니다.

## Important Files

- `AGENTS.md`: 공통 정책, `.opencode-context`, 계약 경계, graphify/plugin/worktree 정책
- `opencode.json`: 로컬 opencode 설정과 graphify plugin 등록
- `.opencode-context/reports/003-bootstrap-installation-guide.md`: 설치/이식 가이드
- `.opencode-context/reports/004-oh-my-opencode-slim-adoption.md`: oh-my-opencode-slim 실험 전략
- `.opencode-context/reports/002-skill-plugin-review.md`: 현재 skill/plugin 검토

## Next Steps

1. 현재 작업트리가 깨끗한지 `git status --short`로 확인합니다.
2. `oh-my-opencode-slim` 실험을 위한 별도 worktree 또는 임시 디렉토리를 만듭니다.
3. 임시 환경에서 `bunx oh-my-opencode-slim@latest install` 결과를 확인합니다.
4. 생성된 config, agent, command, skill, plugin 파일을 현재 템플릿과 비교합니다.
5. 우선순위에 따라 codemap workflow, subtask workflow, session goal/checkpoint workflow, explorer/oracle 계열 prompt를 먼저 검토합니다.
6. 결과를 `.opencode-context/reports/005-oh-my-opencode-slim-diff.md`에 기록합니다.

## Open Questions

- 전체 plugin을 유지할지, 문서/prompt/workflow만 선별 흡수할지 결정이 필요합니다.
- `oh-my-opencode-slim` 설치가 글로벌 설정을 수정하는지 확인해야 합니다.
- model preset을 이 템플릿에 포함할지, 사용자별 글로벌 설정으로 둘지 결정해야 합니다.

## Commands Run

- `graphify --version`
- `python3 -c "import json, pathlib; json.loads(pathlib.Path('opencode.json').read_text()); print('opencode.json: valid JSON')"`
- `git commit -m "chore: initialize opencode defaults template"`

## Risks / Notes

opencode 설정, skill, plugin 변경은 현재 세션에 hot reload되지 않을 수 있으므로 재시작 후 확인합니다.
