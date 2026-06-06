# .opencode-context

opencode와 사용자가 장기 맥락을 Markdown으로 공유하기 위한 디렉토리입니다.

프로젝트 시작 전에 사용자가 미리 정해야 하는 목표, 환경, 스택, 개발 철학은 루트 `PROJECT.md`에 둡니다. `.opencode-context/`는 작업 중 생기는 보고서, 논의 과정, 결정 기록, 세션 체크포인트, 사용자 제공 입력 자료를 보관합니다.

## Structure

- `reports/`: 분석 보고서, 검토 결과, 도입 전략
- `discussions/`: 결정 전 아키텍처 협의 과정, 후보안, 질문, 트레이드오프
- `decisions/`: 의사결정 기록과 ADR
- `sessions/`: 세션 체크포인트, 인계 메모
- `contracts/`: API, DB, 이벤트, public interface, 모듈 경계 문서
- `inbox/`: 사용자가 제공한 임시 입력 파일, 스크린샷, 이미지, PDF, 로그, 텍스트 덤프
- `assets/`: 보고서, 결정 기록, 계약 문서에서 계속 참조할 보존 자료

## Naming

- 보고서, 의사결정, 계약 문서는 `001-short-title.md`처럼 3자리 순번과 짧은 kebab-case 제목을 사용합니다.
- 논의 파일은 `YYYY-MM-DD_HH-MM-SS_short-slug.md` 형식을 사용합니다.
- 세션 체크포인트는 `YYYY-MM-DD_HH-MM-SS_short-slug.md` 형식을 사용합니다.
- inbox 원자료는 날짜별 디렉토리 `.opencode-context/inbox/YYYY-MM-DD/` 아래에 둡니다.
- assets 파일은 짧은 kebab-case 이름을 사용합니다.

## Policy

계약 경계면을 변경할 때는 `.opencode-context/contracts/`의 문서를 먼저 확인하고, 수정 전 사용자 승인을 받아야 합니다.

아키텍처, 기술 스택, 개발 철학, 운영 방식처럼 결정 전 논의가 필요한 내용은 `.opencode-context/discussions/`에 먼저 기록하고, 확정된 판단만 필요 시 `.opencode-context/decisions/`로 승격합니다.

`.opencode-context/inbox/`의 실제 입력 파일은 기본적으로 git에 커밋하지 않습니다. 장기 보존할 자료는 민감정보를 제거한 뒤 `.opencode-context/assets/`로 승격합니다.

VLM 또는 multimodal 분석을 위해 파일을 첨부할 때는 `opencode run --file <path> "<prompt>"` 형식을 사용할 수 있습니다. 실제 이미지/PDF 처리는 사용하는 provider/model의 지원 여부에 따릅니다.

## Bootstrap

다른 환경으로 이식할 때는 `reports/003-bootstrap-installation-guide.md`를 먼저 확인합니다.

`oh-my-opencode-slim` 선별 흡수 방식은 `reports/004-oh-my-opencode-slim-adoption.md`를 기준으로 검토합니다.
