# Local Agents

프로젝트 로컬 opencode agent를 두는 위치입니다.

새 agent는 다음 구조로 추가합니다.

```text
.opencode/agents/<agent-name>.md
```

기본 agent를 override하거나 새 subagent를 만들 때 사용합니다.

현재 로컬 agent:

- `oracle-review`: slim `oracle` prompt를 참고한 read-only 아키텍처/리뷰 advisor
