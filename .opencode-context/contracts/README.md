# Contracts (계약 경계)

API 스키마, DB 스키마, 이벤트 포맷, public interface, 모듈 경계, 인증/권한 경계를 기록하는 위치입니다.

계약 경계면의 추가, 삭제, 이름 변경, 의미 변경, 호환성 변경은 사용자 확인 후 진행합니다.

## Naming (이름 규칙)

계약 문서는 다음 형식을 사용합니다.

```text
001-short-title.md
```

순번은 디렉토리 내에서 증가시키고, 제목은 짧은 kebab-case로 작성합니다.

## Template (템플릿)

```md
# Contract (계약): short-title

## Boundary (경계)

이 문서가 다루는 API, DB, 이벤트, public interface, 모듈, 인증/권한 경계를 적습니다.

## Current Shape (현재 형태)

현재 필드, 엔드포인트, 타입, 권한, 모듈 책임을 적습니다.

## Change Rules (변경 규칙)

어떤 변경이 사용자 확인을 필요로 하는지 적습니다.

## Compatibility (호환성)

기존 데이터, 외부 소비자, 마이그레이션 필요 여부를 적습니다.

## Verification (검증)

계약 변경 시 필요한 테스트, 리뷰, 마이그레이션 검증을 적습니다.
```
