# oh-my-opencode-slim Adoption Options

작성일: 2026-06-06

## 결론

`oh-my-opencode-slim`은 전체 설치해서 사용하는 것도 현실적인 선택입니다. 다만 이 템플릿을 장기적으로 안정적인 기본값으로 만들려면, 전체 설치를 바로 커밋하기보다 별도 환경에서 설치 결과를 관찰하고 필요한 부분을 선별 흡수하는 방식이 좋습니다.

## 왜 선별 흡수가 어려운가

`oh-my-opencode-slim`은 단순 skill 묶음이 아니라 opencode orchestration plugin입니다. agent routing, model preset, MCP, subtask, session workflow, codemap 등 여러 요소가 함께 동작합니다.

따라서 일부만 가져오려면 기능을 다음 단위로 분해해야 합니다.

- agent prompt
- command
- skill
- plugin hook
- MCP 설정
- model preset
- 문서화된 workflow

## 옵션 1: 전체 설치 후 관찰

가장 빠른 방법입니다.

장점은 다음입니다.

- 바로 사용 가능합니다.
- author가 의도한 routing과 workflow를 그대로 경험할 수 있습니다.
- 어떤 기능이 실제로 유용한지 빨리 판단할 수 있습니다.

단점은 다음입니다.

- 글로벌 설정이 바뀔 수 있습니다.
- model preset과 agent 구성이 템플릿 정책과 충돌할 수 있습니다.
- plugin이 tool 사용 흐름에 영향을 줄 수 있습니다.
- 나중에 걷어내기가 어려울 수 있습니다.

이 옵션을 쓸 경우 별도 worktree 또는 테스트 계정에서 먼저 실행하는 것을 추천합니다.

```bash
bunx oh-my-opencode-slim@latest install
```

## 옵션 2: 설치 결과 diff 후 cherry-pick

가장 추천하는 방식입니다.

절차는 다음입니다.

1. 깨끗한 임시 디렉토리나 worktree를 만듭니다.
2. `oh-my-opencode-slim`을 설치합니다.
3. 생성된 config, agent, command, skill, plugin 파일을 확인합니다.
4. 현재 템플릿과 diff를 봅니다.
5. 필요한 항목만 복사합니다.
6. 복사한 항목마다 목적과 권한 범위를 문서화합니다.

이 방식은 전체 설치의 사용감을 보존하면서도 템플릿의 통제력을 유지합니다.

## 옵션 3: 문서와 prompt만 참고

가장 보수적인 방식입니다.

가져올 후보는 다음입니다.

- codemap workflow
- subtask workflow
- session goal workflow
- explorer/oracle/fixer 같은 agent prompt 구조
- MCP 사용 정책 문서

plugin 자체는 설치하지 않고, 현재 opencode 기본 agent와 local skill로 유사한 workflow만 구현합니다.

## 옵션 4: 전체 plugin은 사용하되 템플릿에는 기록만

개인 환경에서는 전체 plugin을 쓰고, 이 저장소에는 설치 절차와 권장 preset만 기록하는 방식입니다.

장점은 템플릿이 가볍게 유지된다는 점입니다. 단점은 다른 환경에서 재현성이 낮다는 점입니다.

## 선별 흡수 우선순위

먼저 가져올 만한 항목은 다음입니다.

1. codemap workflow
2. subtask workflow
3. session goal 또는 checkpoint workflow
4. explorer 계열 코드베이스 탐색 agent
5. oracle 계열 아키텍처 검토 agent

나중에 검토할 항목은 다음입니다.

1. full orchestrator plugin
2. council multi-model workflow
3. websearch/context7/grep_app MCP
4. background subagent 기능
5. preset switching

## 현재 템플릿에서의 추천

현재는 `graphify`, `git`, `git-worktree`, `tidy-tdd-first`, `.opencode-context`만으로도 기본 골격은 충분합니다.

다음 단계에서는 `oh-my-opencode-slim`을 직접 설치하기보다, 임시 환경에서 설치 결과를 분석한 보고서를 먼저 작성하는 것이 좋습니다.

추천 보고서 경로는 다음입니다.

```text
.opencode-context/reports/005-oh-my-opencode-slim-diff.md
```

그 다음 실제로 가져올 파일을 결정합니다.
