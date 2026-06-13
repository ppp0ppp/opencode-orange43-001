# Current OpenCode State

작성일: 2026-06-06

업데이트: 2026-06-13 문서 구조 개편으로 계약 문서는 `docs/contracts/`, 아키텍처 문서는 `docs/architectures/`, 계획 문서는 `docs/plans/`, 논의 문서는 `.project-context/discussions/{draft|open|closed}/`를 사용합니다. 기존 `decision` command와 `.opencode-context/decisions/` 기준 설명은 더 이상 현재 정책이 아닙니다.

## 결론

현재 이 저장소의 opencode 상태는 정상입니다. `opencode debug config` 기준으로 프로젝트 로컬 설정이 의도대로 로드되고 있으며, 기본 모델과 small model은 모두 `openai/gpt-5.5`입니다.

구성 방향은 보수적입니다. 프로젝트 로컬 설정을 중심으로 `graphify` plugin과 로컬 skills를 사용하고, `oh-my-opencode-slim`은 전체 plugin 설치가 아니라 `simplify` skill과 `oracle-review` subagent만 선별 흡수한 상태입니다.

## 확인 범위

- opencode CLI version: `1.16.2`
- 프로젝트 설정: `opencode.json`
- 전역 설정: `~/.config/opencode/opencode.jsonc`
- 로컬 agent: `.opencode/agents/`
- 로컬 skill: `.opencode/skills/`
- 로컬 plugin: `.opencode/plugins/graphify.js`
- resolved config: `opencode debug config`
- available skills: `opencode debug skill`
- available agents: `opencode agent list`
- git 상태: `git status --short`, `git log --oneline -3`

## 설정 로드 상태

전역 설정은 현재 `$schema`만 포함합니다.

```json
{
  "$schema": "https://opencode.ai/config.json"
}
```

따라서 실제 동작 기준은 프로젝트 `opencode.json`입니다. `opencode debug config`에서 확인된 핵심 값은 다음입니다.

- `model`: `openai/gpt-5.5`
- `small_model`: `openai/gpt-5.5`
- `logLevel`: `INFO`
- `share`: `manual`
- `autoupdate`: `notify`
- `snapshot`: `true`
- `instructions`: `AGENTS.md`
- `skills.paths`: `.opencode/skills`
- `plugin`: `file:///home/orange43/project/test/.opencode/plugins/graphify.js`
- `tool_output.max_lines`: `2000`
- `tool_output.max_bytes`: `51200`
- `compaction.auto`: `true`
- `compaction.tail_turns`: `4`
- `compaction.prune`: `true`

## Permission 상태

전역 permission 정책은 읽기/탐색은 허용하고, 수정/외부 접근/네트워크성 작업은 보수적으로 제한하는 형태입니다.

허용되는 주요 읽기 도구:

- `read`: `allow`
- `glob`: `allow`
- `grep`: `allow`
- `list`: `allow`
- `skill`: `allow`
- `task`: `allow`
- `todowrite`: `allow`
- `question`: `allow`

문의가 필요한 작업:

- `edit`: `ask`
- `webfetch`: `ask`
- `websearch`: `ask`
- `external_directory`: 기본 `ask`

외부 디렉터리 차단:

- `~/.ssh/**`: `deny`
- `~/.gnupg/**`: `deny`
- `~/secrets/**`: `deny`

Bash 정책:

- 기본: `*`는 `ask`
- 읽기성 명령: `ls*`, `pwd`, `git status*`, `git diff*`, `git log*`, `git branch*`는 `allow`
- 테스트 명령: `npm test*`, `pnpm test*`, `bun test*`, `pytest*`는 `allow`
- 파괴적 명령: `rm *`, `rm -rf *`, `git reset --hard*`, `git clean *`, `git checkout -- *`, `git restore *`, `sudo *`는 `deny`

최근 실제 테스트에서 `build`, `plan`, `oracle-review` 모두 `git status --short`와 `git log --oneline -3` 같은 읽기 bash 명령을 권한 문의 없이 실행했습니다.

## Agent 상태

현재 사용 가능한 핵심 agent 구조는 다음입니다.

- `build`: primary agent, 프로젝트 설정에서 `edit: ask`로 보수적 수정 권한 유지
- `plan`: primary agent, 프로젝트 설정에서 `edit: deny`로 계획 전용 성격 강화
- `explore`: built-in subagent 유지
- `general`: built-in subagent 유지
- `oracle-review`: 프로젝트 로컬 subagent

`oracle-review`는 `.opencode/agents/oracle-review.md`에서 정의됩니다.

역할:

- 아키텍처 판단
- 복잡한 디버깅 조언
- 코드 리뷰
- 단순화/YAGNI 검토
- 엔지니어링 tradeoff 검토

권한:

- `read`, `glob`, `grep`, `list`: `allow`
- `edit`: `deny`
- `task`: `deny`
- `todowrite`: `deny`
- `webfetch`, `websearch`: `ask`
- `bash`: 기본 `ask`, 읽기성 `ls*`, `pwd`, `git status*`, `git diff*`, `git log*`, `git branch*`만 `allow`

평가:

`oracle-review`는 read-only advisor로 적절히 제한되어 있습니다. 구현을 맡기지 않고 판단/리뷰에 쓰는 현재 정책과 일치합니다.

## Skill 상태

`opencode debug skill`과 로컬 파일 기준으로 다음 skills가 노출됩니다.

- `git`: Conventional Commits와 Git Flow 기반 branch/commit workflow
- `git-worktree`: worktree 기반 병렬 작업 환경 관리
- `tidy-tdd-first`: TDD, regression reproduction, Tidy First workflow
- `simplify`: 동작 보존 code simplification과 readability 개선
- `graphify`: knowledge graph 생성과 query/path/explain workflow
- `customize-opencode`: opencode 설정/agent/skill/plugin 수정 시 사용하는 built-in skill

`simplify`는 `oh-my-opencode-slim@1.1.1`에서 독립적으로 흡수한 local skill입니다. full slim plugin, MCP, model preset, `.slim` state에는 의존하지 않습니다.

평가:

현재 skill 구성은 중복이 과하지 않습니다. `tidy-tdd-first`는 개발 프로세스, `simplify`는 동작 보존 정리, `git`/`git-worktree`는 변경 관리, `graphify`는 구조 이해를 담당합니다.

## Plugin 상태

현재 프로젝트 plugin은 하나입니다.

- `.opencode/plugins/graphify.js`

resolved config에서는 다음 file URL로 로드됩니다.

```text
file:///home/orange43/project/test/.opencode/plugins/graphify.js
```

plugin 동작:

- `tool.execute.before` hook을 사용합니다.
- `graphify-out/graph.json`이 존재할 때 최초 bash 호출 앞에 graphify query 사용 안내를 삽입합니다.
- 현재 `graphify-out/graph.json`이 존재하므로, 새 opencode 실행/도구 호출 흐름에서는 최초 bash 호출 앞에 graphify query 안내가 삽입될 수 있습니다.

의존성:

- `.opencode/package.json`에 `@opencode-ai/plugin: 1.16.2`가 등록되어 있습니다.

평가:

현재 plugin은 범위가 작고, graph가 있을 때 안내성 prefix만 추가합니다. 다만 `tool.execute.before` hook은 bash command를 실제로 수정하므로, 향후 plugin을 늘릴 때는 동일 hook 충돌 여부를 확인해야 합니다.

## Command 상태

프로젝트 `opencode.json`에는 다음 command template이 정의되어 있습니다.

- `review`: 현재 변경사항을 code review 관점으로 점검
- `plan-change`: 수정 전 구현 계획 작성
- `checkpoint`: `.project-context/sessions/`에 세션 체크포인트 작성
- `handoff`: 이어받기용 handoff note 작성
- `discussion`: `.project-context/discussions/draft/`에 structured discussion 작성

평가:

command 구성은 현재 문서 운영 정책과 일치합니다. 보고서, 논의, 세션 체크포인트를 분리하고 확정 판단은 `docs/`의 공식 문서로 흡수하는 현재 AGENTS.md 정책과도 맞습니다.

## graphify 상태

현재 `graphify-out/graph.json`은 생성되어 있습니다. 따라서 코드베이스 질문에는 graphify query fast path를 사용할 수 있습니다.

정책상 다음이 적용됩니다.

- 코드베이스 질문에서는 먼저 `graphify query` 사용
- 관계 질문에서는 `graphify path` 사용
- 개념 설명에는 `graphify explain` 사용
- broad architecture review가 아니면 `GRAPH_REPORT.md`를 직접 크게 읽지 않음
- 코드 수정 후 graph가 존재하면 `graphify update .` 제안 또는 실행

평가:

현재 graphify skill, plugin, graph 산출물이 모두 준비된 상태입니다. `graphify update .` 실행 결과 code graph가 생성되었고, `graphify-out/GRAPH_REPORT.md` 기준 368 nodes, 331 edges, 42 communities가 확인되었습니다. LLM 토큰 비용은 0입니다.

## oh-my-opencode-slim 흡수 상태

현재 흡수된 항목:

- `simplify` skill
- `oracle-review` subagent
- slim 관련 판단/보류 정책 문서화

보류된 항목:

- full `oh-my-opencode-slim` plugin
- TUI plugin 등록
- built-in `explore`/`general` 비활성화
- model preset 기본값 추가
- MCP 서버 `websearch`, `context7`, `grep_app`
- `agent-browser` 글로벌 설치
- `council` multi-model workflow
- background/multiplexer workflow
- `.slim` 상태 디렉터리와 codemap script

평가:

현재 흡수 범위가 적절합니다. 추가 흡수는 실제 불편이 생긴 뒤 `fixer` 스타일 bounded implementation agent 정도만 검토하면 됩니다. 지금 더 가져오면 설정 복잡도와 hook/MCP 충돌 위험이 이득보다 큽니다.

## Git 상태

확인 시점의 `git status --short`는 다음 변경을 표시했습니다.

```text
 M .opencode/agents/README.txt
 M .opencode/skills/README.md
 M AGENTS.md
 M README.md
 M opencode.json
?? .project-context/reports/005-oh-my-opencode-slim-diff.md
?? .project-context/reports/006-slim-absorption-branch.md
?? .opencode/agents/oracle-review.md
?? .opencode/skills/simplify/
```

최근 커밋:

```text
5074aee chore: refine opencode context workflow
5cf7772 chore: initialize opencode defaults template
```

이 보고서 작성으로 새 파일이 추가됩니다.

```text
.project-context/reports/007-current-opencode-state.md
```

주의:

위 dirty worktree 항목 대부분은 기존 opencode 템플릿/oh-my-opencode-slim 선별 흡수 작업의 결과로 보입니다. 이 보고서 작성 과정에서는 해당 파일들을 되돌리거나 수정하지 않았습니다.

## 리스크와 주의사항

1. Config-time 파일 변경 후 재시작 필요

opencode는 config, agent, skill, plugin 파일을 시작 시 로드합니다. `opencode.json`, `.opencode/agents/`, `.opencode/skills/`, `.opencode/plugins/`를 변경한 뒤에는 opencode를 재시작해야 새 세션에 확실히 반영됩니다.

2. Plugin hook은 작아도 실행 경로에 영향 가능

`graphify.js`는 현재 작고 안전한 편이지만 bash command를 수정하는 hook입니다. 향후 plugin을 추가할 때 hook 순서와 command 변조 충돌을 확인해야 합니다.

3. Permission rule 순서 유지 필요

bash permission은 broad `* : ask` 뒤에 narrow allow/deny가 오는 구조입니다. opencode permission matching은 마지막 매칭 rule이 중요하므로, 향후 편집 시 broad rule과 deny rule의 위치를 주의해야 합니다.

4. Built-in agent permission 병합 확인 필요

`opencode agent list` 출력상 built-in agent에는 기본 permission과 프로젝트 permission, agent별 override가 함께 나타납니다. 현재 읽기 bash 테스트는 통과했지만, 새 agent override를 추가할 때는 반드시 resolved permission을 다시 확인해야 합니다.

5. graphify graph는 생성물이며 git 추적 대상이 아님

`graphify-out/graph.json`은 생성되어 있지만 git status에는 나타나지 않습니다. 현재 정책상 graphify 생성물은 local-only 산출물로 다루며 커밋하지 않습니다. 코드나 문서 변경 후에는 `graphify update .`로 최신성을 유지해야 합니다.

## 권장 운영 방식

- 일반 구현: `build` 사용, 수정은 permission `ask` 흐름 유지
- 수정 전 계획: `plan` 또는 `plan-change` command 사용
- 코드 리뷰/아키텍처 판단: `oracle-review` 사용
- 동작 보존 리팩터링: `simplify` skill 사용
- TDD/회귀 재현: `tidy-tdd-first` skill 사용
- git 작업: `git` skill과 `git-worktree` skill 사용
- 장기 구조 이해: graph 생성 후 `graphify query/path/explain` 사용
- 큰 작업 종료 또는 인계: `checkpoint`/`handoff` command 사용
- 계약 경계 변경: `docs/contracts/` 확인 후 사용자 승인 필요

## 검증 결과

실행한 확인 명령:

```bash
opencode --version
opencode debug config
opencode debug skill
opencode agent list
git status --short
git log --oneline -3
```

이전 권한 smoke test 결과:

- `build` agent: `ls`, `git status --short`, `git log --oneline -3` 권한 문의 없이 실행됨
- `plan` agent: `ls`, `git status --short`, `git log --oneline -3` 권한 문의 없이 실행됨
- `oracle-review` subagent: `git status --short`, `git log --oneline -3` 권한 문의 없이 실행됨

최종 판단:

현재 opencode 상태는 사용 가능한 안정 상태입니다. 추가 slim 흡수, MCP 활성화, full plugin 도입, agent 대체는 지금 필요하지 않습니다. 현 상태를 기준선으로 유지하고, 실제 워크플로우 병목이 확인될 때만 작은 단위로 확장하는 것이 좋습니다.
