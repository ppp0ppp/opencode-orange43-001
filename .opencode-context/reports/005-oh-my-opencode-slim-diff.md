# oh-my-opencode-slim Install Diff

작성일: 2026-06-06

## 결론

`oh-my-opencode-slim@1.1.1`은 이 템플릿에 전체 설치하기보다 필요한 workflow와 skill만 선별 흡수하는 편이 안전합니다.

전체 installer는 단순 파일 추가가 아니라 글로벌 opencode 설정에 plugin을 등록하고, TUI 설정을 수정하고, 기본 내장 agent 일부를 비활성화하고, LSP를 켜며, 별도 preset config를 생성합니다. 현재 템플릿의 `graphify`, 내장 `explore/general`, 보수적 permission 정책과 충돌 가능성이 있습니다.

## 실행 환경

- 패키지: `oh-my-opencode-slim@1.1.1`
- installer 런타임: Bun 필요
- 현재 셸 PATH에는 `bun`이 없었지만 `~/.bun/bin/bun`은 사용 가능했습니다.
- 실제 설치는 아래 격리 경로로 제한했습니다.
- `HOME=/tmp/opencode/oms-home`
- `XDG_CONFIG_HOME=/tmp/opencode/oms-config`
- `XDG_CACHE_HOME=/tmp/opencode/oms-cache`
- `OPENCODE_CONFIG_DIR=/tmp/opencode/oms-config/opencode`
- `OPENCODE_TUI_CONFIG=/tmp/opencode/oms-config/opencode/tui.json`

## 실행한 명령

```bash
bun --version
"$HOME/.bun/bin/bun" --version
PATH="$HOME/.bun/bin:$PATH" npx --yes oh-my-opencode-slim@latest --help
mkdir -p "/tmp/opencode/oms-home" "/tmp/opencode/oms-config/opencode" "/tmp/opencode/oms-cache"
PATH="$HOME/.bun/bin:$PATH" HOME="/tmp/opencode/oms-home" XDG_CONFIG_HOME="/tmp/opencode/oms-config" XDG_CACHE_HOME="/tmp/opencode/oms-cache" OPENCODE_CONFIG_DIR="/tmp/opencode/oms-config/opencode" OPENCODE_TUI_CONFIG="/tmp/opencode/oms-config/opencode/tui.json" npx --yes oh-my-opencode-slim@latest install --no-tui --skills=no --dry-run
PATH="$HOME/.bun/bin:$PATH" HOME="/tmp/opencode/oms-home" XDG_CONFIG_HOME="/tmp/opencode/oms-config" XDG_CACHE_HOME="/tmp/opencode/oms-cache" OPENCODE_CONFIG_DIR="/tmp/opencode/oms-config/opencode" OPENCODE_TUI_CONFIG="/tmp/opencode/oms-config/opencode/tui.json" npx --yes oh-my-opencode-slim@latest install --no-tui --skills=no
```

## 생성 파일

격리 설치 결과는 다음입니다.

```text
/tmp/opencode/oms-config/opencode/opencode.json
/tmp/opencode/oms-config/opencode/opencode.json.bak
/tmp/opencode/oms-config/opencode/tui.json
/tmp/opencode/oms-config/opencode/oh-my-opencode-slim.json
/tmp/opencode/oms-cache/opencode/packages/oh-my-opencode-slim@latest/
```

`/tmp/opencode/oms-config/opencode/opencode.json`:

```json
{
  "plugin": ["oh-my-opencode-slim"],
  "agent": {
    "explore": { "disable": true },
    "general": { "disable": true }
  },
  "lsp": true
}
```

`/tmp/opencode/oms-config/opencode/tui.json`:

```json
{
  "plugin": ["oh-my-opencode-slim"]
}
```

`/tmp/opencode/oms-config/opencode/oh-my-opencode-slim.json`:

- `$schema`: `https://unpkg.com/oh-my-opencode-slim@latest/oh-my-opencode-slim.schema.json`
- active preset: `openai`
- generated presets: `openai`, `opencode-go`
- agents: `orchestrator`, `oracle`, `librarian`, `explorer`, `designer`, `fixer`, plus `council` and `observer` in `opencode-go`

## Installer 동작

확인된 installer 단계는 다음입니다.

1. OpenCode 설치 여부 확인
2. `opencode.json`의 `plugin` 배열에 `oh-my-opencode-slim` 추가
3. `tui.json`의 `plugin` 배열에 `oh-my-opencode-slim` 추가
4. OpenCode plugin cache warm-up
5. 기본 내장 agent `explore`, `general` 비활성화
6. `lsp`가 없으면 `true`로 설정
7. `oh-my-opencode-slim.json` preset config 생성

`--skills=yes` 기본값을 쓰면 추가로 recommended/bundled skill 설치가 실행됩니다. recommended skill인 `agent-browser`는 `npm install -g agent-browser`와 `agent-browser install` post-install command를 포함하므로, 이 템플릿에서는 사용자 승인 없이 실행하지 않는 것이 맞습니다.

## 현재 템플릿과의 차이

현재 템플릿은 다음 구조입니다.

- project `opencode.json` 중심 설정
- `.opencode/plugins/graphify.js`만 project plugin으로 등록
- `.opencode/skills`에는 `graphify`, `git`, `git-worktree`, `tidy-tdd-first`
- 내장 `explore/general` agent는 유지
- bash/edit/webfetch/websearch는 보수적 permission
- `graphify-out/`은 local-only 생성물

`oh-my-opencode-slim` 전체 설치와 충돌하거나 판단이 필요한 부분은 다음입니다.

- `plugin`: orchestration plugin을 추가하면 tool/agent/session 흐름에 hook 영향이 생깁니다.
- `agent.explore/general.disable`: 현재 기본 agent 사용 전제와 다릅니다.
- `lsp: true`: 현재 템플릿은 LSP를 강제하지 않습니다.
- `tui.json`: 템플릿에는 TUI 설정 정책이 아직 없습니다.
- model preset: `openai/gpt-5.5`, `openai/gpt-5.4-mini`, `opencode-go/*`를 템플릿 기본값으로 둘지 결정해야 합니다.
- MCP: `websearch`, `context7`, `grep_app`를 agent별로 사용합니다. 현재 정책상 외부 backend와 권한 범위 확인이 필요합니다.

## 포함된 Skill 후보

패키지 tarball에 포함된 bundled skill은 다음입니다.

- `codemap`: `.slim/codemap.json`과 각 디렉토리 `codemap.md`를 사용해 계층형 codemap을 생성합니다.
- `simplify`: 동작 보존 refactor와 readability 개선 workflow입니다.
- `clonedeps`: 중요한 dependency source를 `.slim/clonedeps/repos/` 아래에 clone하는 workflow입니다.

추천 흡수 순서는 다음입니다.

1. `simplify`: 현재 `tidy-tdd-first`와 철학이 잘 맞고 plugin 의존성이 없습니다.
2. `codemap` 문서 일부: 현재 graphify 정책과 중복되므로 `.slim` state와 script를 그대로 가져오기보다 “폴더별 요약 지도” workflow만 참고합니다.
3. `clonedeps`: 네트워크 clone과 외부 repo 보존 정책이 필요하므로 보류합니다.

## Agent/Workflow 후보

번들된 agent prompt에서 참고할 만한 최소 아이디어는 다음입니다.

- `explorer`: 넓은 codebase 탐색을 병렬화하고 요약만 반환합니다. 현재 내장 `explore` agent와 역할이 유사합니다.
- `oracle`: 아키텍처 판단, code review, YAGNI/simplification 검토에 집중합니다. 별도 read-only review agent 후보입니다.
- `fixer`: 충분히 좁혀진 구현 작업만 수행하고 연구/위임을 금지합니다. 대규모 작업에서 bounded implementation subagent로 참고할 수 있습니다.
- `subtask` workflow: parent context를 절약하기 위해 self-contained prompt와 compact result를 주고받는 방식입니다. 현재 `task` tool 운용 규칙에 문서로 흡수할 수 있습니다.
- `session goal`: `/goal` command로 목표를 고정하고 todo/delegation/verification을 정렬합니다. 현재 `.opencode-context/sessions` checkpoint 정책과 결합 가능성이 있습니다.

## 보류 항목

다음 항목은 지금 템플릿에 바로 넣지 않는 것이 좋습니다.

- full orchestrator plugin
- `tui.json` plugin 등록
- `explore/general` 비활성화
- model preset 기본값
- `websearch`, `context7`, `grep_app` MCP 기본 활성화
- `agent-browser` 글로벌 설치
- `council` multi-model workflow
- background/tmux/zellij/multiplexer workflow
- `.slim` 상태 디렉토리 도입

## 권장 다음 단계

1. `simplify` skill을 `.opencode/skills/simplify/SKILL.md`로 가져올지 결정합니다.
2. `oracle` 계열 read-only review subagent를 project agent로 만들지 결정합니다.
3. codemap은 graphify와 역할을 나눌지 먼저 결정합니다.
4. `oh-my-opencode-slim` 전체 plugin은 별도 개인 환경이나 worktree에서 사용감을 더 확인한 뒤 결정합니다.
5. Bun을 계속 쓸 경우 shell profile에 `~/.bun/bin` PATH가 반영되었는지 새 터미널에서 확인합니다.

## 검증 결과

- `oh-my-opencode-slim@latest --help` 실행 성공
- 격리 dry-run 실행 성공
- 격리 실제 install 실행 성공
- 실제 프로젝트 `opencode.json`과 글로벌 `~/.config/opencode`는 이 실험에서 직접 수정하지 않았습니다.
- `graphify-out/graph.json`이 없어 graphify update는 생략합니다.
