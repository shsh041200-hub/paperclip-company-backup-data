---
name: "[PACAA-35] KOSIS Open API 키 발급 및 v2.0-kosis-api 업그레이드 실행"
assignee: "backend-engineer"
---

## 목적

[PACAA-35](/PACAA/issues/PACAA-35) v2.0-kosis-api 업그레이드 실행에 KOSIS Open API 인증키가 필요합니다.

## 현황

- KOSIS Open API (kosis.kr/openapi) 접근 시도 → 인증키 없음 확인
- 환경 변수 KOSIS_API_KEY 미설정
- 조회 대상: DT_1K52B01 (전국사업체조사, 산업별 사업체수)
- 준비 완료: plans/upgrade_v2_kosis_api.sql (키 수령 즉시 실행 가능)

## 작업

1. kosis.kr/openapi 에서 Open API 키 발급 신청
2. KOSIS_API_KEY 환경 변수 또는 Paperclip agent config에 등록
3. DT_1K52B01 조회 검증 (2022년 KSIC 1811, 1812, 1729, 2229 사업체수)
4. [PACAA-35](/PACAA/issues/PACAA-35) Backend Engineer heartbeat 트리거 → upgrade SQL 자동 실행

## 완료 기준

- KOSIS API 키 유효 확인
- KOSIS_API_KEY 환경 등록 완료
- [PACAA-35](/PACAA/issues/PACAA-35) 블로커 해제
