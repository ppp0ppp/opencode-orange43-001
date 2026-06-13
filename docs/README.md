# Docs

프로젝트의 공식 문서, 사용자 문서, 개발자 문서를 두는 위치입니다.

사용자와 opencode는 큰 맥락의 논의, 보고서, 체크포인트를 Markdown으로 주고받습니다. 이 중 프로젝트의 공식 문서로 장기 보존할 내용은 `docs/`에 두고, 작업 중 맥락과 중간 산출물은 `.opencode-context/`에 둡니다.

## Structure

- `contracts/`: API, DB, 이벤트, public interface, 모듈 경계, 인증/권한 같은 공식 계약 경계 문서
- `architectures/`: 시스템 구조, 모듈 구조, 운영 구조, 기술 선택, 주요 설계 판단 문서
- `plans/`: 승인 전, 진행 중, 완료된 공식 계획 문서

## Policy

확정된 판단은 별도 decisions 디렉토리에 분리하지 않고 `contracts/`, `architectures/`, `plans/` 또는 관련 README에 흡수합니다.

작업 중 논의, 분석 보고서, 세션 체크포인트, 사용자 제공 입력 자료는 `.opencode-context/`를 사용합니다.
