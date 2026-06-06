# .opencode-context

opencode와 사용자가 장기 맥락을 Markdown으로 공유하기 위한 디렉토리입니다.

## Structure

- `reports/`: 분석 보고서, 검토 결과, 도입 전략
- `decisions/`: 의사결정 기록과 ADR
- `sessions/`: 세션 체크포인트, 인계 메모
- `contracts/`: API, DB, 이벤트, public interface, 모듈 경계 문서

## Naming

파일명은 `001-short-title.md`처럼 3자리 순번과 짧은 kebab-case 제목을 사용합니다.

## Policy

계약 경계면을 변경할 때는 `.opencode-context/contracts/`의 문서를 먼저 확인하고, 수정 전 사용자 승인을 받아야 합니다.

## Bootstrap

다른 환경으로 이식할 때는 `reports/003-bootstrap-installation-guide.md`를 먼저 확인합니다.

`oh-my-opencode-slim` 선별 흡수 방식은 `reports/004-oh-my-opencode-slim-adoption.md`를 기준으로 검토합니다.
