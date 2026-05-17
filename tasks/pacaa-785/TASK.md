---
name: "[O1] 공공데이터 cross-validation — BRN PRIMARY KEY 화 + 국세청/공정위 API 통합"
assignee: "backend-engineer"
---

## 목적
PACAA-784 결정 (보드 2026-05-17 ask_user_questions answered):
- 현재 크롤링 품질 약점 W3 (BRN-주소-웹사이트 cross-validate 부재) 해결
- W5 (단일 소스 의존) 부분 완화

## 작업
1. 공공데이터포털 **사업자등록정보 진위확인 API** (국세청, 무료) 통합 → `vendor_brn_checks` 강화
2. **공정위 통신판매업 신고 데이터** (Excel 정기 다운로드 또는 공개 API) → 별도 reference 테이블
3. `companies.brn` 을 PRIMARY identification key 로 승격 — `vendor_candidates` / `vendor_brn_checks` / `vendor_domain_checks` 모두 BRN join
4. 매칭 파이프라인에 BRN cross-check 추가: 동일 BRN 이 사업자명·주소·웹사이트와 일치하는지 검증
5. Audit JSON 에 cross-validation 결과 (`brn_verified`, `address_match`, `cross_source_count`) 필드 추가

## Acceptance Criteria
- 국세청 BRN 진위확인 API live 통합 (휴/폐업 상태 동기화)
- 공정위 통신판매업 데이터 최소 월 1회 업데이트 (cron or manual script)
- 기존 `companies.website` 가 BRN cross-check 실패하면 audit 에 `cross_validation_failed` 플래그
- Dry-run 실행 후 false positive/negative 베이스라인 보고

## 제약
- Legal P0-B 4-필드 제약 유지 (이름·전화·주소·카테고리)
- 추가 PII 수집 금지
- 비용: $0 (모두 무료 공공 API)
- 일정: 3~5일

## 부모 이슈
PACAA-784 (https://packlinx.com/...)
