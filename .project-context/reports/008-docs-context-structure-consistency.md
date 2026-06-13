# Docs And Context Structure Consistency Review

작성일: 2026-06-13

## 결론

요청된 방향은 전체적으로 타당합니다. `docs/`를 프로젝트 공식 문서의 기준 위치로 두고, `.opencode-context/`를 opencode와 사용자 간의 작업 맥락, 논의, 보고서, 세션, 입력 자료 중심으로 축소하면 문서의 장기 보존성과 임시 작업 맥락이 더 명확하게 분리됩니다.

권장 최종 구조는 다음과 같습니다.

- `docs/contracts/`: 공식 계약 경계 문서
- `docs/architectures/`: 공식 아키텍처 문서
- `docs/plans/`: 승인 전, 진행 중, 완료된 계획 문서
- `.opencode-context/discussions/`: 초안, 진행 중, 종료된 논의 문서
- `.opencode-context/reports/`: 분석 보고서, 검토 결과, 제안서
- `.opencode-context/sessions/`: 세션 체크포인트와 인계 메모
- `.opencode-context/inbox/`: 사용자 제공 임시 입력 자료
- `.opencode-context/assets/`: 작업 중 계속 참조할 보존 자료

핵심 판단은 다음과 같습니다.

- `.opencode-context/decisions/`는 삭제해도 됩니다.
- 단, `.opencode-context/decisions/001-opencode-context-directory.md`의 배경은 완전 폐기하지 말고 `docs/README.md` 또는 `.opencode-context/README.md`에 흡수하는 편이 좋습니다.
- `contracts`와 `architectures`는 압축적이고 순서가 중요한 공식 문서이므로 `001-short-title.md`를 유지하는 편이 좋습니다.
- `plans`와 `discussions`는 상태 이동과 시간 추적성이 중요하므로 `YYYY-MM-DD_HH-MM-SS_detail-title.md`가 더 적합합니다.
- README의 문서 리스팅은 우선 수동 목록으로 충분합니다. 새 문서 추가, 이동, 종료 시 작성자가 직접 갱신하는 방식입니다.
- `reports`와 `sessions`는 현재처럼 `.opencode-context/` 아래에 유지하는 편이 좋습니다.

## 배경

현재 문서 구조는 `.opencode-context/`가 보고서, 논의, 결정 기록, 세션, 계약 문서를 모두 보관하는 형태입니다. 이 구조는 opencode와 사용자 간의 작업 맥락을 한곳에 모으는 데는 유리하지만, 계약 문서와 확정 아키텍처처럼 프로젝트 공식 문서에 가까운 자료까지 숨김 디렉토리에 들어가는 문제가 있습니다.

사용자는 다음 방향을 제안했습니다.

- `.opencode-context/decisions` 삭제
- `.opencode-context/contracts`를 `docs/contracts`로 이동
- `docs/architectures` 추가
- `docs/plans`와 상태별 하위 디렉토리 추가
- `.opencode-context/discussions`를 상태별 하위 디렉토리로 재정렬
- 승인 전에는 루트 논의 문서와 보고서를 통해 구조를 검토

이 보고서는 추가/수정 파일 목록만이 아니라, 새 구조가 전체 문서 정책과 어떻게 맞아야 하는지 검토합니다.

## 권장 정보 구조

```text
docs/
  README.md
  contracts/
    README.md
    001-short-title.md
  architectures/
    README.md
    001-short-title.md
  plans/
    README.md
    scheduled/
      YYYY-MM-DD_HH-MM-SS_detail-title.md
    open/
      YYYY-MM-DD_HH-MM-SS_detail-title.md
    closed/
      YYYY-MM-DD_HH-MM-SS_detail-title.md

.opencode-context/
  README.md
  discussions/
    README.md
    draft/
      YYYY-MM-DD_HH-MM-SS_detail-title.md
    open/
      YYYY-MM-DD_HH-MM-SS_detail-title.md
    closed/
      YYYY-MM-DD_HH-MM-SS_detail-title.md
  reports/
    001-short-title.md
  sessions/
    YYYY-MM-DD_HH-MM-SS_short-slug.md
  inbox/
  assets/
```

삭제 대상:

```text
.opencode-context/decisions/
```

이동 대상:

```text
.opencode-context/contracts/ -> docs/contracts/
```

## 책임 경계

`docs/`의 책임:

- 프로젝트 공식 문서를 둡니다.
- 계약, 아키텍처, 계획처럼 장기적으로 참조될 문서를 둡니다.
- opencode 전용 맥락이 아니어도 사람이 직접 읽고 판단할 수 있어야 하는 문서를 둡니다.

`.opencode-context/`의 책임:

- opencode와 사용자가 작업 중 교환하는 맥락을 둡니다.
- 분석 보고서, 논의, 세션 체크포인트, 사용자 입력 자료를 둡니다.
- 공식 문서로 승격되기 전의 중간 산출물을 둡니다.

`reports`의 책임:

- 사용자가 판단해야 하는 분석, 검토, 제안을 남깁니다.
- 공식 계약 또는 아키텍처 자체가 아니라, 그것을 만들기 위한 조사와 판단 근거를 남깁니다.
- 보고서 내용이 확정 규칙이 되면 `docs/contracts`, `docs/architectures`, `docs/plans` 또는 관련 README로 흡수합니다.

`sessions`의 책임:

- 작업 인계와 재개에 필요한 짧은 체크포인트를 둡니다.
- 공식 결정 기록이나 논의 본문을 대체하지 않습니다.

## 파일명 규칙 판단

`contracts`와 `architectures`:

- 권장 형식: `001-short-title.md`
- 이유: 문서 수가 많아지지 않아야 하고, 독자가 정해진 순서로 읽는 편이 유리합니다.
- 성격: 압축적, 공식적, 장기 보존형 문서입니다.

`plans`와 `discussions`:

- 권장 형식: `YYYY-MM-DD_HH-MM-SS_detail-title.md`
- 기준 시각: 최초 생성 시각입니다.
- 이유: 문서가 상태 디렉토리 사이를 이동할 수 있고, 시간적 추적성이 중요합니다.
- 성격: 상태 전이가 있으며, 동시 진행과 이력 파악이 중요합니다.

`reports`:

- 기존 형식인 `001-short-title.md`를 유지하는 편이 좋습니다.
- 보고서는 상태 이동보다 축적된 검토 결과의 순서가 더 중요합니다.

`sessions`:

- 기존 형식인 `YYYY-MM-DD_HH-MM-SS_short-slug.md`를 유지하는 편이 좋습니다.
- 세션은 시간순 재개와 인계가 핵심입니다.

## README 리스팅 방식

README의 문서 리스팅은 우선 수동 목록으로 두는 것을 권장합니다.

여기서 수동 목록은 새 문서를 만들거나 상태 디렉토리를 옮길 때 작성자가 README의 목록을 직접 갱신한다는 뜻입니다.

자동 리스팅을 지금 도입하지 않는 이유:

- 별도 스크립트나 CI가 필요해지고 구조 변경보다 도구 관리가 커질 수 있습니다.
- 현재 문서 수가 많지 않습니다.
- `plans`와 `discussions`는 상태 이동 시 사람이 문서 의미를 확인해야 하므로 자동화 이점이 제한적입니다.

## 계획 문서 정책

위치:

- `docs/plans/scheduled/`: 아직 미승인 또는 실행 전 계획서
- `docs/plans/doing/`: 실행 중인 계획서
- `docs/plans/archived/`: 모든 계획이 완료 또는 중단 처리된 계획서

필수 섹션:

- `## 상태`: `scheduled`, `doing`, `archived` 중 하나
- `## 작업 범위`: 본 계획서의 포함 범위와 제외 범위
- `## Plan Ground`: 일반적으로 분류된 체크리스트 목록
- `## Plan Tree`: 단계적 트리 형식 체크리스트 목록
- `## Checklist`: 전체 체크리스트 목록과 상태
- `## 근거 및 영향 문서`: 근거 문서와 영향받을 문서 레퍼런스

체크리스트 형식:

```md
- [ ] CL-001: 항목 설명 (pending)
- [ ] CL-002: 항목 설명 (now doing)
- [x] CL-003: 항목 설명 (done)
- [ ] CL-004: 항목 설명 (aborted)
```

상태 값:

- `done`: 완료
- `now doing`: 현재 진행 중
- `pending`: 대기
- `aborted`: 중단 또는 폐기

정합성 판단:

- 계획서의 디렉토리 상태와 본문 `## 상태`는 항상 일치해야 합니다.
- 상태 이동 시 파일명은 바꾸지 않고 최초 생성 시각을 유지합니다.
- 계획서 동시 진행 수는 제한하지 않되, 서로 영향을 주는 계획은 `근거 및 영향 문서`에 명시해야 합니다.

## 논의 문서 정책

위치:

- `.opencode-context/discussions/draft/`: 초안, 미정의, 에이전트의 초안 제시
- `.opencode-context/discussions/open/`: 사용자와 에이전트가 질문/답변과 논의로 문서를 완성하는 중
- `.opencode-context/discussions/closed/`: 논의가 끝났고 공식 문서로 흡수된 상태

필수 섹션:

- `## 상태`: `draft`, `open`, `closed` 중 하나
- `## 범위`: 본 논의 문서의 포함 범위와 제외 범위
- `## 분석`: 배경, 문제, 관찰, 리스크
- `## 추천 전략/계획/옵션`: 추천안 또는 대안
- `## 질문`: 사용자 확인이 필요한 사항
- `## 근거 및 영향 문서`: 근거 문서와 영향받을 문서 레퍼런스

정합성 판단:

- 논의 문서의 디렉토리 상태와 본문 `## 상태`는 항상 일치해야 합니다.
- `closed` 논의는 독립적인 최종 결정 문서 역할을 하면 안 됩니다.
- 닫힌 논의의 결론은 `docs/contracts`, `docs/architectures`, `docs/plans`, 관련 README 중 하나 이상에 흡수되어야 합니다.

## decisions 삭제 판단

`.opencode-context/decisions/` 삭제는 타당합니다.

이유:

- 결정 기록은 계약, 아키텍처, 계획 문서와 중복될 가능성이 큽니다.
- 별도 ADR 계층을 유지하면 문서가 세 갈래로 분산될 수 있습니다.
- 현재 프로젝트 규모에서는 공식 문서에 결정 내용을 직접 흡수하는 편이 더 단순합니다.

단, 기존 `.opencode-context/decisions/001-opencode-context-directory.md`의 핵심 배경은 흡수하는 편이 좋습니다.

흡수할 핵심 내용:

- 사용자와 opencode는 큰 맥락의 논의, 보고서, 체크포인트를 Markdown으로 주고받습니다.
- `.opencode-context/`는 opencode와 사용자 사이의 작업 맥락 전용 공간입니다.
- 공식 프로젝트 문서와 작업 중 맥락은 분리합니다.

흡수 위치 권장:

- `docs/README.md`: `docs/`가 공식 문서 위치라는 원칙을 명시합니다.
- `.opencode-context/README.md`: `.opencode-context/`가 작업 맥락과 중간 산출물 위치라는 원칙을 명시합니다.

## 현재 문서와의 충돌 지점

`AGENTS.md`:

- `Context Files`에서 의사결정 기록을 `.opencode-context/decisions/`에 둔다고 설명합니다.
- 계약/스키마 문서를 `.opencode-context/contracts/`에 둔다고 설명합니다.
- 보고서, 의사결정, 계약 문서 파일명을 모두 `001-short-title.md`로 묶고 있습니다.
- 논의 파일 위치를 `.opencode-context/discussions/YYYY-MM-DD_HH-MM-SS_short-slug.md`로 직접 지정하고 있어 상태 하위 디렉토리와 충돌합니다.
- `Architecture Discussions`에서 확정된 결정을 `.opencode-context/decisions/`로 승격한다고 설명합니다.
- `Contract Boundaries`에서 계약 문서 기준 위치를 `.opencode-context/contracts/`로 둡니다.
- `Graphify Policy` 섹션이 두 번 존재합니다. 이번 구조 변경의 직접 대상은 아니지만, AGENTS를 수정할 때 함께 정리할 가치가 있습니다.

`docs/README.md`:

- 계약 문서를 `.opencode-context/`에 둔다고 설명합니다.
- 새 구조에서는 `docs/`가 계약, 아키텍처, 계획의 공식 위치가 되어야 하므로 수정이 필요합니다.

`.opencode-context/README.md`:

- `decisions/`와 `contracts/`를 구조에 포함합니다.
- 확정된 판단을 `.opencode-context/decisions/`로 승격한다고 설명합니다.
- 계약 경계면 변경 시 `.opencode-context/contracts/`를 먼저 확인한다고 설명합니다.

`.opencode-context/reports/README.md`:

- 장기적으로 확정된 결정은 `.opencode-context/decisions/`로 기록한다고 설명합니다.
- 계약 경계면 관련 내용은 `.opencode-context/contracts/`에 반영한다고 설명합니다.
- 새 구조에서는 각각 `docs/architectures`, `docs/plans`, `docs/contracts` 등을 참조해야 합니다.

`.opencode-context/discussions/README.md`:

- 기존 상태 값이 `Draft | In Discussion | Decided | Superseded`입니다.
- 새 상태 값인 `draft | open | closed`와 상태 하위 디렉토리 구조로 재작성해야 합니다.
- 확정 결론을 `.opencode-context/decisions/`로 승격한다는 설명을 제거해야 합니다.

`.opencode-context/assets/README.md`:

- 보고서, 결정 기록, 계약 문서에서 참조할 자료라고 설명합니다.
- 새 구조에서는 결정 기록 대신 공식 문서, 계약, 아키텍처, 계획 문서에서 참조할 자료라고 표현하는 편이 일관됩니다.

`.opencode-context/sessions/README.md`:

- 관련 discussion/decision 경로를 적는다고 설명합니다.
- `decision` 경로 언급은 공식 문서 또는 discussion/plan/contract/architecture 경로로 바꾸는 편이 좋습니다.

## 권장 수정 범위

승인 후 한 번에 정리할 것을 권장하는 파일과 디렉토리입니다.

디렉토리 변경:

- `.opencode-context/decisions/` 삭제
- `.opencode-context/contracts/`를 `docs/contracts/`로 이동
- `docs/architectures/` 생성
- `docs/plans/scheduled/` 생성
- `docs/plans/doing/` 생성
- `docs/plans/archived/` 생성
- `.opencode-context/discussions/draft/` 생성
- `.opencode-context/discussions/open/` 생성
- `.opencode-context/discussions/closed/` 생성

문서 수정 또는 추가:

- `docs/README.md`
- `docs/contracts/README.md`
- `docs/architectures/README.md`
- `docs/plans/README.md`
- `.opencode-context/README.md`
- `.opencode-context/discussions/README.md`
- `.opencode-context/reports/README.md`
- `.opencode-context/sessions/README.md`
- `.opencode-context/assets/README.md`
- `AGENTS.md`

선택 수정:

- 루트 `docs-context-restructure-discussion.md`를 사용자의 답변 기준으로 갱신하거나, 승인 후 `.opencode-context/discussions/closed/`로 이동할 수 있습니다.

## 구현 순서 제안

1. `docs/contracts`를 만들고 `.opencode-context/contracts`의 내용을 이동합니다.
2. `docs/architectures`, `docs/plans`와 하위 상태 디렉토리를 추가합니다.
3. `.opencode-context/discussions` 하위 상태 디렉토리를 추가합니다.
4. `.opencode-context/decisions/001-opencode-context-directory.md`의 핵심 배경을 `docs/README.md`와 `.opencode-context/README.md`에 흡수합니다.
5. `.opencode-context/decisions/`를 삭제합니다.
6. 각 README의 목적, 파일명 규칙, 문서 리스팅을 새 구조에 맞게 갱신합니다.
7. `AGENTS.md`의 Context Files, Architecture Discussions, Contract Boundaries 지침을 새 구조에 맞게 갱신합니다.
8. `AGENTS.md`의 중복 `Graphify Policy` 섹션을 하나로 합칠지 별도 확인합니다.
9. `git status`로 이동, 삭제, 추가 파일을 확인합니다.

## 리스크

- `AGENTS.md`는 opencode의 실제 행동 지침에 영향을 주므로, 문서 구조 변경 승인 후 함께 고치지 않으면 새 구조와 실행 지침이 계속 충돌합니다.
- `decisions` 삭제 후 결정의 근거가 공식 문서에 흡수되지 않으면 왜 그렇게 결정했는지 추적하기 어려워질 수 있습니다.
- `plans`와 `discussions`는 상태 디렉토리와 본문 상태가 불일치할 수 있으므로 이동 시 README 리스팅과 본문 상태를 함께 갱신해야 합니다.
- 문서 리스팅을 수동으로 유지하면 누락 가능성이 있습니다. 다만 현재 규모에서는 자동화보다 수동 관리가 더 단순합니다.

## 제안

이번 구조 변경은 단순 파일 이동이 아니라 문서 책임 경계 변경이므로, 승인 후 `AGENTS.md`까지 포함해 정합성을 맞추는 편이 좋습니다.

권장 정책은 다음과 같습니다.

- 공식 문서: `docs/`
- 작업 맥락: `.opencode-context/`
- 확정 판단: 별도 `decisions`가 아니라 `docs/contracts`, `docs/architectures`, `docs/plans`, README에 흡수
- 논의 종료 조건: 결론이 공식 문서로 흡수됨
- 계획 종료 조건: 모든 체크리스트가 `done` 또는 명시적으로 `aborted` 처리됨

## 후속 질문

- 루트 `docs-context-restructure-discussion.md`는 승인 후 `.opencode-context/discussions/closed/`로 이동할까요, 아니면 루트 임시 문서로 두었다가 삭제할까요?
- `AGENTS.md`의 중복 `Graphify Policy` 섹션도 이번 정합성 수정에 포함할까요?
- `docs/plans`의 `scheduled`는 미승인만 의미할까요, 아니면 승인됐지만 아직 착수하지 않은 계획도 포함할까요?
