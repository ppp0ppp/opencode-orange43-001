# Discussion: main/dev 브랜치 기반 템플릿 운영 전략

## Status (상태)

closed

## Summary (요약)

이 논의는 저장소의 `main`과 `dev` 브랜치를 서로 다른 목적의 작업면으로 분리하는 운영 규칙을 정리합니다.

최종 결론은 `main`을 바로 클론해서 사용할 수 있는 깨끗한 템플릿 브랜치로 유지하고, `dev`에는 현재와 같은 논의, 계획, 보고서, 세션 등 구조 생성 과정과 운영 이력을 남기는 것입니다.

추가 개발은 `feat/xxx` 브랜치에서 진행한 뒤 `dev`로 병합하고, `main`에는 규약 문서, 디렉토리 구조, 공용 tool/skill/plugin 업데이트처럼 템플릿 사용자에게 필요한 최소 산출물만 선별 반영합니다.

## Background (배경)

현재 저장소에는 `.project-context/`, `docs/plans/`, 논의 문서, 보고서, 세션 체크포인트처럼 하네스가 만들어지는 과정과 의사결정의 이력이 남아 있습니다. 이 이력은 개발자와 유지보수자에게 유용하지만, 사용자가 저장소를 바로 클론해 새 프로젝트 템플릿으로 쓰기에는 과한 맥락이 될 수 있습니다.

사용자는 다음 브랜치 구성을 제안했습니다.

- `main`: 현재 문서들이 남지 않고, `.gitkeep` 정도로 디렉토리 구조만 미리 만들어둔 템플릿 브랜치
- `dev`: 현재 문서와 구조 생성 과정, 논의/계획/보고서/세션 이력이 남는 개발 브랜치
- `feat/xxx`: 새 기능, 규칙, 문서, skill, plugin 등을 실험하고 완성하는 작업 브랜치

또한 `main`의 루트 `README.md`에는 구조 생성 과정이 궁금하면 `dev` 브랜치를 참고하라는 간단한 안내를 남기려 합니다.

## Context (맥락)

현재 프로젝트는 Intent-Anchored Development용 opencode thin agent harness입니다. 핵심 구조는 다음과 같습니다.

- `README.md`: 템플릿 개념과 사용 규칙
- `AGENTS.md`: 에이전트 행동 지침
- `PROJECT.md`: 프로젝트별 목표와 제약을 사용자가 채우는 입력 문서
- `docs/`: 공식 계약, 아키텍처, 계획 문서
- `.project-context/`: 논의, 보고서, 세션, inbox, assets 등 맥락 수집과 근거 보관 공간
- `.opencode/`: project-local skill, agent, plugin
- `opencode.json`: opencode 설정

최근 결정된 원칙에 따르면 `.project-context/`는 실행 기준이 아니라 맥락 수집과 근거 보관 공간입니다. 따라서 템플릿 사용자가 바로 시작하는 `main`에는 과거 맥락 파일을 많이 남기지 않는 편이 목적과 잘 맞습니다.

## Scope (범위)

포함:

- `main`, `dev`, `feat/*` 브랜치 역할 정의
- `main`에 남길 문서와 파일의 범위 정의
- `dev`에 남길 개발 이력과 문서의 범위 정의
- `feat/* -> dev -> main` 반영 흐름 정의
- `main` README에 넣을 브랜치 안내 문구 후보 정리
- 확정 시 반영 대상 문서 후보 정리

제외:

- 지금 즉시 브랜치를 생성하거나 재작성하는 작업
- `main`에서 기존 문서를 삭제하는 작업
- 실제 merge, rebase, cherry-pick 실행
- release/tag 전략 상세 설계
- GitHub Actions 또는 자동 동기화 구성

## Constraints (제약)

- `main`은 바로 클론해 템플릿으로 사용할 수 있어야 합니다.
- `main`은 디렉토리 구조를 유지하기 위해 필요한 경우 `.gitkeep`을 사용할 수 있습니다.
- `main`에는 사용자가 새 프로젝트에서 바로 쓰는 데 필요한 규약 문서와 공용 기능만 남겨야 합니다.
- `dev`는 구조 생성 과정, 논의, 계획, 보고서, 세션 체크포인트를 보존할 수 있어야 합니다.
- 새 변경은 원칙적으로 `feat/xxx`에서 만들고, 완성 후 `dev`로 병합합니다.
- `main`에는 `dev` 전체를 그대로 병합하지 않고 템플릿 사용자에게 필요한 결과만 선별 반영합니다.
- 브랜치 정책은 루트 `README.md`와 `AGENTS.md` 또는 별도 공식 문서 중 적절한 위치에 흡수해야 합니다.

## Analysis (분석)

`main`과 `dev`를 같은 내용으로 유지하면 사용자에게는 저장소의 전체 역사와 작업 맥락이 노출됩니다. 이는 투명성에는 좋지만, 템플릿 사용성에는 불리합니다. 특히 `.project-context/reports/`, `.project-context/discussions/closed/`, `.project-context/sessions/`는 특정 시점의 근거와 인계 체크포인트이므로 새 프로젝트의 초기 상태로 남기기에는 부적절할 수 있습니다.

반대로 `main`을 너무 비우면 템플릿 사용자가 어떤 규칙으로 이 구조를 써야 하는지 알기 어렵습니다. 따라서 `main`은 빈 저장소가 아니라 "즉시 사용 가능한 최소 템플릿"이어야 합니다.

`dev`는 이 하네스 자체를 진화시키는 개발 브랜치로 두는 것이 자연스럽습니다. 새 규칙, 문서 구조, skill, plugin, workflow는 `feat/*`에서 만들고, 논의/계획/검증을 거쳐 `dev`에 전체 이력을 남깁니다. 이후 `main`에는 사용자에게 필요한 최종 규칙과 빈 구조만 선별해 반영합니다.

핵심은 `main`과 `dev`를 단순한 배포/개발 브랜치로만 보지 않고, 서로 다른 독자를 가진 브랜치로 보는 것입니다.

- `main`의 독자: 새 프로젝트에 템플릿을 적용하려는 사용자
- `dev`의 독자: 템플릿 자체를 유지보수하고 발전시키는 사용자/에이전트

## Options (대안)

옵션 A: `main`과 `dev`를 거의 동일하게 유지합니다.

- 장점: 병합이 단순합니다.
- 장점: 모든 문맥이 항상 보입니다.
- 단점: `main`이 템플릿으로 쓰기에는 지저분해집니다.
- 단점: `.project-context/`의 과거 문맥이 새 프로젝트의 기준처럼 보일 수 있습니다.

옵션 B: `main`은 깨끗한 템플릿, `dev`는 전체 개발 이력 보존 브랜치로 분리합니다.

- 장점: `main`을 바로 클론해 사용할 수 있습니다.
- 장점: `dev`에서 구조 생성 과정과 의사결정 이력을 보존할 수 있습니다.
- 장점: `.project-context/`가 새 프로젝트에 과도하게 섞이는 문제를 줄입니다.
- 단점: `dev`에서 `main`으로 선별 반영하는 관리 비용이 생깁니다.
- 단점: 두 브랜치의 차이를 문서화하지 않으면 기여 흐름이 혼란스러울 수 있습니다.

옵션 C: `main`은 템플릿, 별도 `history` 또는 `docs-history` 브랜치에 이력을 보존합니다.

- 장점: `dev`를 일반 개발 브랜치로 가볍게 유지할 수 있습니다.
- 단점: 브랜치가 늘어나고 운영 규칙이 복잡해집니다.
- 단점: 사용자가 제안한 `dev` 중심 흐름보다 설명 비용이 큽니다.

옵션 D: 템플릿 배포용 별도 태그나 release artifact를 만듭니다.

- 장점: `main`을 개발 브랜치로 유지하면서도 깨끗한 배포물을 제공할 수 있습니다.
- 단점: 릴리스 자동화나 수동 패키징 규칙이 필요합니다.
- 단점: 현재 단계에서는 과한 운영 방식일 수 있습니다.

## Trade-offs (트레이드오프)

옵션 B는 템플릿 사용성과 개발 이력 보존을 동시에 만족합니다. 다만 `dev`에서 `main`으로 전체 병합하지 않는다는 원칙 때문에, 매번 어떤 파일을 `main`에 반영할지 판단해야 합니다.

이 판단을 줄이려면 `main`에 남길 파일 범위를 명확히 해야 합니다.

`main`에 남길 후보:

- `README.md`: 템플릿 사용법, 브랜치 안내, 최소 workflow
- `AGENTS.md`: 에이전트 기본 행동 규칙
- `PROJECT.md`: 사용자가 채울 프로젝트 입력 템플릿
- `opencode.json`: project-local opencode 설정
- `.opencode/`: 공용 agents, skills, plugins, README
- `docs/README.md`, `docs/contracts/README.md`, `docs/architectures/README.md`, `docs/plans/README.md`
- `.project-context/README.md`와 하위 디렉토리 README
- 빈 디렉토리 유지를 위한 `.gitkeep`
- 라이선스, `.gitignore`, 필요한 최소 설정 파일

`main`에서 비우거나 제외할 후보:

- `.project-context/discussions/*`의 실제 논의 문서
- `.project-context/reports/*`의 실제 보고서
- `.project-context/sessions/*`의 실제 세션 체크포인트
- `docs/plans/{scheduled,doing,archived}/*`의 실제 계획서
- 특정 실험이나 과거 상태를 담은 문서

`dev`에 남길 후보:

- 위의 모든 운영 이력
- 논의/계획/보고서/세션
- 실험 결과와 후보안
- `feat/*` 병합 이력

## Recommended Strategy / Plan / Options (추천 전략/계획/옵션)

추천안은 옵션 B입니다.

브랜치 역할:

- `main`: 바로 클론해서 사용할 수 있는 깨끗한 템플릿 브랜치
- `dev`: 템플릿 자체의 개발 이력, 논의, 계획, 보고서, 세션을 보존하는 브랜치
- `feat/xxx`: 새 규칙, 문서, skill, plugin, workflow를 만드는 작업 브랜치

병합 흐름:

- 새 변경은 `feat/xxx`에서 시작합니다.
- 완성된 변경은 `dev`에 전체 병합합니다.
- `main`에는 `dev` 전체를 병합하지 않고, 템플릿 사용자에게 필요한 최종 산출물만 선별 반영합니다.
- `main`에는 규약 문서, 빈 디렉토리 구조, `.gitkeep`, 공용 tool/skill/plugin 업데이트만 유지합니다.

`main` README 안내 문구 후보:

```md
## Branches

`main` is the clean template branch. It keeps the reusable rules, opencode configuration, shared agents/skills/plugins, and empty directory structure for new projects.

The discussion history, planning history, reports, and session checkpoints used to design this template live on `dev`. If you want to understand why the structure exists or how it evolved, inspect the `dev` branch.

New changes are developed in `feat/*`, merged into `dev`, and then selectively promoted to `main` only when they are useful for the reusable template.
```

한국어 README라면 다음처럼 쓸 수 있습니다.

```md
## Branches

`main`은 바로 클론해서 사용할 수 있는 깨끗한 템플릿 브랜치입니다. 재사용 가능한 규칙, opencode 설정, 공용 agents/skills/plugins, 빈 디렉토리 구조만 유지합니다.

이 템플릿의 구조가 만들어진 과정, 논의, 계획, 보고서, 세션 체크포인트는 `dev` 브랜치에 남깁니다. 구조의 배경이 궁금하면 `dev` 브랜치를 확인합니다.

새 변경은 `feat/*`에서 만들고 `dev`에 병합한 뒤, 재사용 가능한 템플릿 산출물만 `main`에 선별 반영합니다.
```

## Decision Candidate (결정 후보)

아직 확정 전이지만 현재 결정 후보는 다음과 같습니다.

- `main`은 깨끗한 템플릿 브랜치로 유지합니다.
- `main`에는 실제 논의, 보고서, 세션, 완료 계획 문서를 남기지 않습니다.
- `main`에는 필요한 디렉토리 구조를 `.gitkeep` 또는 README로 유지합니다.
- `main`에는 규약 문서, opencode 설정, 공용 agents/skills/plugins, 최소 README를 유지합니다.
- `dev`는 현재와 같은 문서와 생성 과정을 보존하는 개발 브랜치로 둡니다.
- 새 작업은 `feat/xxx`에서 시작하고 완성 후 `dev`에 병합합니다.
- `main`에는 `dev`의 전체 이력이 아니라 템플릿 사용자에게 필요한 최종 산출물만 선별 반영합니다.
- `main` 루트 README에는 구조 생성 과정이 궁금하면 `dev` 브랜치를 참고하라는 안내를 넣습니다.

## Questions (질문)

- `main`에서 `.project-context/README.md`와 하위 디렉토리 README는 유지하고 실제 문서만 제거하는 방식이 맞습니까?
  답변: 맞습니다. README는 구조 설명에 필요하고, 실제 문서만 제거합니다.
- `docs/plans/README.md`는 유지하되 `scheduled/`, `doing/`, `archived/` 내부는 `.gitkeep`만 둘까요?
  답변: 맞습니다. README는 유지하고 하위 상태 디렉토리는 `.gitkeep`로 유지합니다.
- `main`에서 `.project-context/reports/README.md`는 유지할까요, 아니면 reports 디렉토리 자체를 `.gitkeep`만 두고 README도 최소화할까요?
  답변: `reports/README.md`는 유지하되, 보고서는 main에 기본 포함하지 않는다는 점을 명시합니다.
- `main`에 `.opencode/skills/graphify`와 `.opencode/plugins/graphify.js` 같은 공용 기능은 그대로 유지할까요?
  답변: 유지합니다. graphify skill/plugin은 공용 기능입니다. 단, hook/MCP/외부 backend는 기본 비활성 유지합니다.
- `dev -> main` 선별 반영은 cherry-pick, checkout path, 별도 release branch 중 어떤 방식으로 운용할까요?
  답변: 초기에는 `checkout path` 방식으로 운용합니다. `dev`에서 필요한 파일만 `main`으로 가져옵니다.
- 이 브랜치 정책은 `README.md`만으로 충분할까요, 아니면 `AGENTS.md`와 `docs/`에도 반영할까요?
  답변: `README.md`에 간략 명시하고, `AGENTS.md`에는 작업 규칙으로 짧게 반영합니다.

## Open Issues (열린 쟁점)

- `main`에서 제거할 실제 문서 목록과 유지할 템플릿 README 목록을 확정해야 합니다.
  정리: 계획서에서 제거/유지 목록을 확정합니다.
- `main`의 빈 디렉토리 구조를 `.gitkeep`으로 유지할지, README 파일로 유지할지 정해야 합니다.
  정리: README가 필요한 디렉토리는 README를 유지하고, 빈 상태 디렉토리는 `.gitkeep`로 유지합니다.
- `dev` 브랜치가 아직 없다면 생성 기준과 시작점을 정해야 합니다.
  정리: 계획서에서 현재 main 상태를 dev 보존 시작점으로 삼는 절차를 다룹니다.
- `main`을 깨끗하게 만들 때 기존 이력을 보존하는 방식과 merge 전략을 정해야 합니다.
  정리: dev에 현재 이력을 보존하고 main은 선별 정리합니다.
- 이후 `feat/*` 브랜치 명명 규칙과 커밋/병합 규칙을 `AGENTS.md`에 반영할지 결정해야 합니다.
  정리: AGENTS에 짧게 반영합니다.

## Resolution (정리 결과)

사용자 승인에 따라 다음 결론으로 확정합니다.

- `main`은 바로 클론 가능한 깨끗한 템플릿 브랜치로 유지합니다.
- `dev`는 현재 문서, 논의, 계획, 보고서, 세션 등 생성 과정과 운영 이력을 보존하는 개발 브랜치로 둡니다.
- 새 작업은 `feat/xxx`에서 시작하고 완성 후 `dev`에 병합합니다.
- `main`에는 `dev` 전체를 병합하지 않고 재사용 가능한 최종 산출물만 선별 반영합니다.
- `main`에는 실제 논의, 보고서, 세션, 완료 계획 문서를 남기지 않습니다.
- `main`에는 `README.md`, `AGENTS.md`, `PROJECT.md`, `opencode.json`, `.opencode/` 공용 기능, `docs/`와 `.project-context/`의 구조 README, 빈 디렉토리 유지 파일을 남깁니다.
- `.project-context/README.md`와 하위 README는 유지하되 실제 문서는 제거합니다.
- `docs/plans/README.md`는 유지하고 상태 디렉토리는 `.gitkeep`로 유지합니다.
- `reports/README.md`는 유지하되, 보고서는 main에 기본 포함하지 않는다고 명시합니다.
- graphify skill/plugin은 공용 기능으로 유지합니다. hook/MCP/외부 backend는 기본 비활성으로 유지합니다.
- `dev -> main` 선별 반영은 초기에는 checkout path 방식으로 운용합니다.
- 브랜치 정책은 `README.md`에 간략 명시하고, `AGENTS.md`에는 작업 규칙으로 짧게 반영합니다.

이 결론은 다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_16-00-11_branch-template-strategy.md`

## Absorption Target (흡수 대상)

다음 계획서로 흡수합니다.

- `docs/plans/scheduled/2026-06-13_16-00-11_branch-template-strategy.md`

계획 실행 후 다음 문서 또는 브랜치 상태에 반영합니다.

- `README.md`
- `AGENTS.md`
- `main`, `dev`, `feat/*` 브랜치 운영 상태

## References (근거 및 영향 문서)

근거:

- 사용자 요청: `main`은 깨끗한 템플릿 브랜치, `dev`는 현재 문서와 생성 과정을 보존하는 브랜치로 운영
- 사용자 요청: 새 작업은 `feat/xxx`에서 만들고 `dev`에 병합, `main`에는 공용 템플릿 산출물만 선별 반영
- `README.md`
- `AGENTS.md`
- `.project-context/README.md`
- `docs/plans/README.md`

영향:

- `README.md`
- `AGENTS.md`
- 브랜치 구성: `main`, `dev`, `feat/*`
- 향후 `main` 정리 계획
- 향후 `dev` 생성 또는 갱신 계획
