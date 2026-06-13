# slim Absorption Branch Notes

작성일: 2026-06-06

## 결론

`feature/oh-my-opencode-slim-absorption`에서는 `oh-my-opencode-slim` 전체 plugin을 설치하지 않고, 독립적으로 안전한 구성요소만 흡수합니다.

이번 실험의 1차 흡수 대상은 다음입니다.

- `simplify` skill: plugin, MCP, model preset 의존성이 없습니다.
- `oracle-review` subagent: slim의 `oracle` prompt를 현재 opencode file agent 형식에 맞춘 read-only 검토 agent입니다.
- codemap workflow 정책 메모: `.slim` state와 script는 가져오지 않고, `graphify`와 역할 충돌을 피하는 기준만 문서화합니다.

## 적용한 변경

- `.opencode/skills/simplify/SKILL.md` 추가
- `.opencode/agents/oracle-review.md` 추가
- `.opencode/skills/README.md`에 `simplify` 등록
- `.opencode/agents/README.txt`에 `oracle-review` 등록
- `AGENTS.md`에 slim 선별 흡수 정책과 codemap/graphify 우선순위 보강
- `README.md`에 slim diff/absorption 보고서 링크 추가

## 보류한 항목

- `oh-my-opencode-slim` plugin 등록
- `tui.json` 변경
- 내장 `explore/general` agent 비활성화
- model preset 기본값 추가
- MCP 서버 `websearch`, `context7`, `grep_app` 활성화
- `agent-browser` 글로벌 설치
- `.slim` 상태 디렉토리와 codemap script 도입
- background/multiplexer workflow

## 사용 기준

- 코드 단순화나 리팩터링 검토가 필요하면 `simplify` skill을 사용합니다.
- 아키텍처 판단, 복잡한 디버깅, 리뷰 품질 검토가 필요하면 `oracle-review` agent를 사용합니다.
- 저장소 전체 관계/장기 맥락은 `graphify`를 우선 사용합니다.
- 폴더별 사람이 읽는 요약 지도가 명시적으로 필요할 때만 codemap workflow를 별도 검토합니다.

## 주의

opencode agent/skill 파일은 config-time 파일이므로, 변경 후 새 세션에서 사용하려면 opencode 재시작이 필요합니다.
