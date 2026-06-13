# .project-context

프로젝트 작업 맥락과 에이전트 협업 산출물을 Markdown과 파일로 공유하기 위한 디렉토리입니다.

프로젝트 시작 전에 사용자가 미리 정해야 하는 목표, 환경, 스택, 개발 철학은 루트 `PROJECT.md`에 둡니다. `.project-context/`는 작업 중 생기는 보고서, 논의 과정, 세션 체크포인트, 사용자 제공 입력 자료, 보존 자료를 보관합니다.

공식 프로젝트 문서는 `docs/`에 둡니다. 계약, 아키텍처, 계획처럼 장기적으로 참조할 확정 문서는 `docs/contracts/`, `docs/architectures/`, `docs/plans/`를 사용합니다.

`.project-context/`는 실행 권한을 갖는 공식 기준이 아닙니다. 계획 승인 후 일반 구현 작업은 `PROJECT.md`, `AGENTS.md`, `docs/contracts/`, `docs/architectures/`, 승인된 `docs/plans/`를 기준으로 진행합니다.

## Structure

- `reports/`: 분석 보고서, 검토 결과, 도입 전략
- `discussions/`: 결정 전 협의 과정, 후보안, 질문, 트레이드오프
- `sessions/`: 세션 체크포인트, 인계 메모
- `inbox/`: 사용자가 제공한 임시 입력 파일, 스크린샷, 이미지, PDF, 로그, 텍스트 덤프
- `assets/`: 보고서, 논의, 공식 문서에서 계속 참조할 보존 자료

## Naming

- 보고서 파일은 `001-short-title.md`처럼 3자리 순번과 짧은 kebab-case 제목을 사용합니다.
- 논의 파일은 `.project-context/discussions/{draft|open|closed}/YYYY-MM-DD_HH-MM-SS_detail-title.md` 형식을 사용합니다.
- 세션 체크포인트는 `YYYY-MM-DD_HH-MM-SS_short-slug.md` 형식을 사용합니다.
- inbox 원자료는 날짜별 디렉토리 `.project-context/inbox/YYYY-MM-DD/` 아래에 둡니다.
- assets 파일은 짧은 kebab-case 이름을 사용합니다.

## Policy

계약 경계면을 변경할 때는 `docs/contracts/`의 문서를 먼저 확인하고, 수정 전 사용자 승인을 받아야 합니다.

아키텍처, 기술 스택, 개발 철학, 운영 방식처럼 결정 전 논의가 필요한 내용은 `.project-context/discussions/`에 먼저 기록하고, 확정된 판단은 `docs/contracts/`, `docs/architectures/`, `docs/plans/` 또는 관련 README에 흡수합니다.

계획 작성 중에는 `.project-context/discussions/draft/`와 `.project-context/discussions/open/`을 기본 참조할 수 있습니다. 계획 승인 후 구현 단계에서는 `.project-context/`를 기본 참조하지 않습니다.

`.project-context/reports/`는 특정 시점의 관찰과 근거이며 실행 기준이 아닙니다. 보고서는 사용자가 명시하거나 에이전트가 참조 이유를 설명해 승인받은 경우에만 확인합니다.

장기 작업 시작 시에는 `.project-context/sessions/`의 최신 세션 파일 1개를 기본 참조할 수 있습니다. 단, 세션은 공식 요구사항이나 계획을 대체하지 않는 인계 체크포인트입니다.

`.project-context/inbox/`의 실제 입력 파일은 기본적으로 git에 커밋하지 않습니다. 장기 보존할 자료는 민감정보를 제거한 뒤 `.project-context/assets/`로 승격합니다.

VLM 또는 multimodal 분석을 위해 파일을 첨부할 때는 `opencode run --file <path> "<prompt>"` 형식을 사용할 수 있습니다. 실제 이미지/PDF 처리는 사용하는 provider/model의 지원 여부에 따릅니다.

## Bootstrap

다른 환경으로 이식할 때는 먼저 `README.md`, `PROJECT.md`, `AGENTS.md`, `docs/`를 확인합니다.

`reports/`의 bootstrap, adoption, diff 보고서는 과거 시점의 근거 자료입니다. 계속 필요한 운영 기준은 공식 문서로 승격해 유지합니다.
