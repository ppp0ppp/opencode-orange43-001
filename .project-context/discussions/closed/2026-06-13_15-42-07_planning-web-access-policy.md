# Discussion: 논의/계획 단계 웹 접근 정책

## Status (상태)

closed

## Summary (요약)

이 논의는 에이전트가 논의와 계획 단계에서 필요한 경우 `webfetch`와 `websearch`를 사용할 수 있음을 명시하는 정책을 정리합니다.

최종 결론은 공식 문서, 공식 스키마, provider 문서, 설치 방법, 최신 외부 정보가 필요한 경우 추측하지 않고 웹 확인을 허용하는 것입니다. 사용자는 지금 단계에서는 `webfetch`와 `websearch`를 계속 허용하는 방향을 승인했습니다.

## Background (배경)

현재 프로젝트의 `opencode.json`에는 `webfetch`와 `websearch` 권한이 `ask`로 설정되어 있습니다.

```json
"webfetch": "ask",
"websearch": "ask"
```

실제 세션에서는 `webfetch` 도구가 노출되어 있으며, `https://opencode.ai/`와 `https://opencode.ai/docs`, `https://opencode.ai/config.json`에 대한 접근 테스트가 성공했습니다. 반면 현재 세션에는 직접적인 `websearch` 도구가 노출되어 있지 않아 검색 엔진 질의는 수행하지 못했습니다.

사용자는 논의/계획 단계에서 필요한 경우 웹 접근을 사용할 수 있음을 명시하고 싶다고 했습니다. 또한 현재는 `webfetch`와 `websearch`를 계속 허용하는 방향을 선호한다고 했습니다.

## Context (맥락)

이 프로젝트는 Intent-Anchored Development용 opencode thin agent harness입니다. 하네스의 핵심은 사용자의 의도, 계약 경계, 계획, 공식 문서를 기준점으로 삼아 모델과 provider가 바뀌어도 작업 드리프트를 줄이는 것입니다.

이 목표상 다음 상황에서 웹 확인이 유용합니다.

- opencode 설정 스키마나 permission shape 확인
- 공식 문서의 최신 필드, 옵션, deprecation 확인
- provider/model 기능과 제한 확인
- 설치 명령, CLI 옵션, MCP/plugin 설정 확인
- 외부 도구의 최신 동작과 보안/네트워크 영향 확인

반대로 웹 접근은 외부 전송과 최신 정보 의존 리스크가 있으므로, 무분별한 검색이나 비공식 블로그 기반 판단은 피해야 합니다.

## Scope (범위)

포함:

- 논의 단계에서의 웹 접근 허용 기준
- 계획 단계에서의 웹 접근 허용 기준
- `webfetch`와 `websearch`의 사용 차이 정리
- 공식 출처 우선 원칙 정리
- `opencode.json` 권한 변경 후보 정리
- 확정 시 반영 대상 문서 후보 정리

제외:

- 지금 즉시 `opencode.json` 수정
- 웹 검색 provider 또는 MCP 추가 구현
- 비공식 검색 결과를 자동으로 신뢰하는 정책
- 웹 접근 결과를 `.project-context/reports/`에 별도 저장하는 자동화

## Constraints (제약)

- 민감한 코드, 토큰, 개인정보, 내부 URL을 외부 웹 서비스나 검색 질의로 보내면 안 됩니다.
- 공식 문서, 공식 스키마, 공식 repository, maintainer 문서를 우선합니다.
- 웹 접근 결과는 현재 시점의 외부 정보이므로, 계속 필요한 기준은 `README.md`, `PROJECT.md`, `AGENTS.md`, `docs/`로 흡수해야 합니다.
- `websearch` 권한이 `allow`여도 현재 실행 환경에 도구가 노출되지 않으면 사용할 수 없습니다.
- 웹 접근 실패 시 그 사실을 보고하고 로컬 공식 문서 기준으로 판단해야 합니다.

## Analysis (분석)

현재 `webfetch`는 실제로 사용할 수 있고, 공식 URL을 알고 있을 때 유용합니다. 예를 들어 opencode 설정 필드가 불확실하면 `https://opencode.ai/config.json`을 직접 확인할 수 있습니다.

`websearch`는 권한 설정 항목은 존재하지만, 현재 세션의 도구 목록에는 노출되어 있지 않습니다. 따라서 정책상 허용하더라도 실제 사용 가능 여부는 실행 환경에 따라 달라집니다.

논의/계획 단계에서 웹 접근을 허용하면 다음 장점이 있습니다.

- 외부 도구 설정을 추측하지 않고 확인할 수 있습니다.
- 최신 schema와 공식 문서를 기준으로 계획을 세울 수 있습니다.
- provider/model/tool 차이에 따른 잘못된 가정을 줄일 수 있습니다.

단점과 리스크도 있습니다.

- 웹 검색 결과는 신뢰도가 일정하지 않습니다.
- 검색 질의에 민감한 정보가 포함될 수 있습니다.
- 웹 접근이 너무 쉬우면 로컬 공식 문서와 계획서 흡수가 소홀해질 수 있습니다.

따라서 웹 접근은 논의/계획 단계에서 허용하되, 공식 출처 우선, 민감정보 금지, 결과 흡수 원칙을 함께 둬야 합니다.

## Options (대안)

옵션 A: `webfetch`와 `websearch`를 모두 `ask`로 유지합니다.

- 장점: 매번 사용자 통제가 가능합니다.
- 단점: 논의/계획 중 공식 문서 확인이 잦으면 흐름이 끊깁니다.

옵션 B: `webfetch`만 `allow`, `websearch`는 `ask`로 둡니다.

- 장점: 공식 URL 확인은 빠르게 할 수 있습니다.
- 장점: 검색 질의는 여전히 사용자 승인을 거칩니다.
- 단점: 사용자가 원하는 “계속 허용”과는 다소 다릅니다.

옵션 C: `webfetch`와 `websearch`를 모두 `allow`로 둡니다.

- 장점: 논의/계획 단계에서 공식 문서와 최신 외부 정보를 빠르게 확인할 수 있습니다.
- 장점: 반복 승인 피로가 줄어듭니다.
- 단점: 검색 도구가 실제로 노출되지 않는 환경에서는 `websearch` allow가 효과가 없습니다.
- 단점: 민감정보가 검색 질의에 들어가지 않도록 에이전트 지침이 필요합니다.

추천은 현재 사용자 의도에 맞춰 옵션 C입니다. 단, 웹 접근 사용 규칙은 `AGENTS.md` 또는 `README.md`에 짧게 명시하는 편이 좋습니다.

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안:

- `opencode.json`에서 `webfetch`와 `websearch`를 `allow`로 변경합니다.
- 논의/계획 단계에서 공식 문서, 공식 스키마, provider 문서, 설치/설정 문서 확인이 필요하면 웹 접근을 사용할 수 있다고 명시합니다.
- URL이 명확하면 `webfetch`를 우선 사용합니다.
- 검색 도구가 제공되는 환경이면 `websearch`로 공식 출처를 찾고, 최종 확인은 공식 문서를 `webfetch`로 수행합니다.
- 검색 도구가 없는 환경이면 알려진 공식 URL을 `webfetch`로 확인하거나 사용자에게 URL을 요청합니다.
- 민감한 코드, 토큰, 개인정보, 내부 URL은 검색 질의나 외부 요청에 포함하지 않습니다.
- 웹 접근 결과 중 계속 필요한 운영 기준은 공식 문서로 흡수합니다.

권장 문구 후보:

```md
## Web Access

논의와 계획 단계에서 최신 외부 정보, 공식 스키마, 설정 필드, 설치 방법, provider 문서가 필요한 경우 추측하지 말고 웹 확인을 우선합니다.

- URL이 명확하면 `webfetch`로 공식 문서를 확인합니다.
- 검색 도구가 제공되는 환경이면 `websearch`로 공식 출처를 찾은 뒤, 최종 확인은 공식 문서를 `webfetch`로 수행합니다.
- 검색 도구가 없는 환경에서는 사용자에게 URL을 요청하거나 알려진 공식 URL을 `webfetch`로 확인합니다.
- 민감한 코드, 토큰, 개인정보, 내부 URL은 웹 요청이나 검색 질의에 포함하지 않습니다.
- 웹 접근이 실패하거나 권한이 없으면 그 사실을 보고하고 로컬 공식 문서 기준으로 판단합니다.
```

## Decision Candidate (결정 후보)

아직 확정 전이지만 현재 결정 후보는 다음과 같습니다.

- 논의/계획 단계에서 필요한 경우 `webfetch`와 `websearch` 사용을 허용합니다.
- `opencode.json`의 `webfetch`와 `websearch`를 `allow`로 변경합니다.
- 웹 접근은 공식 출처 우선으로 사용합니다.
- 민감정보를 웹 요청이나 검색 질의에 포함하지 않습니다.
- 검색 도구가 실제로 노출되지 않는 환경에서는 `webfetch`와 사용자 제공 URL로 대체합니다.
- 웹 접근 결과 중 계속 필요한 기준은 공식 문서로 흡수합니다.
- 반영 대상은 `opencode.json`과 `AGENTS.md` 또는 `README.md` 중 적절한 위치입니다.

## Questions (질문)

- 웹 접근 규칙을 `AGENTS.md`에 넣을까요, 루트 `README.md`에 넣을까요, 둘 다에 짧게 나눠 넣을까요?
  답변: 논의/계획 루트 `README.md`에 넣습니다.
- `webfetch`와 `websearch`를 전역적으로 `allow`할까요, 특정 agent에만 허용할까요?
  답변: 전역 허용합니다.
- 웹 접근 결과를 계획서 References에 항상 기록하게 할까요, 중요한 경우에만 기록하게 할까요?
  답변: 일단 항상 기록합니다.
- 비공식 출처를 참고할 때 사용자 승인이나 별도 표시를 요구할까요?
  답변: 네. 비공식 출처는 사용자 승인이나 별도 표시가 필요합니다.

## Open Issues (열린 쟁점)

- 현재 세션에는 `websearch` 도구가 노출되어 있지 않습니다. 권한을 `allow`로 바꿔도 도구가 없으면 사용할 수 없습니다.
- 웹 검색 질의에 민감한 정보가 들어가지 않도록 에이전트 지침이 필요합니다.
- 웹 접근 결과가 공식 문서로 흡수되지 않으면 외부 정보 의존 드리프트가 생길 수 있습니다.

## Resolution (정리 결과)

사용자 승인에 따라 다음 결론으로 확정합니다.

- 논의/계획 단계에서 필요한 경우 `webfetch`와 `websearch` 사용을 허용합니다.
- `opencode.json`의 `webfetch`와 `websearch`를 전역 `allow`로 변경합니다.
- 웹 접근 규칙은 루트 `README.md`에 반영합니다.
- 웹 접근 결과는 계획서 `References`에 항상 기록합니다.
- `References`에는 원문 전체가 아니라 URL, 공식/비공식 여부, 확인 목적을 짧게 기록합니다.
- 비공식 출처는 사용자 승인 또는 별도 표시를 요구합니다.
- 검색 결과 자체를 근거로 삼기보다, `websearch`로 공식 출처를 찾고 `webfetch`로 공식 문서를 확인합니다.
- 민감한 코드, 토큰, 개인정보, 내부 URL은 웹 요청이나 검색 질의에 포함하지 않습니다.

이 결론은 다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_15-47-57_planning-web-access-policy.md`

## Absorption Target (흡수 대상)

다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_15-47-57_planning-web-access-policy.md`

계획 실행 후 다음 문서 또는 설정에 반영합니다.

- `opencode.json`
- `README.md`
- `docs/plans/README.md`

## References (근거 및 영향 문서)

근거:

- 사용자 요청: 논의/계획 단계에서 `webfetch`와 `websearch` 사용 가능성을 명시
- 사용자 선호: 지금은 `webfetch`와 `websearch`를 계속 허용
- `opencode.json`
- 공식 schema: `https://opencode.ai/config.json`
- 공식 docs: `https://opencode.ai/docs`

영향:

- `opencode.json`
- `README.md`
- `docs/plans/README.md`
- 논의/계획 단계의 외부 정보 확인 방식
