---
name: "[CTO 승인 요청] PACAA-785 — BRN cross-validation 스키마 변경"
assignee: "cto"
---

## 스키마 변경 내역 (CTO 사인오프 필요)

**파일:** `supabase/migrations/20260517001_brn_cross_validation.sql`
**커밋:** `2a0e310`

### 변경 1 — companies.business_registration_number UNIQUE INDEX
```sql
CREATE UNIQUE INDEX companies_brn_unique_idx
  ON companies(business_registration_number)
  WHERE business_registration_number IS NOT NULL;
```
- 현재 모두 NULL → 즉각 영향 없음; 향후 중복 BRN 삽입 방지

### 변경 2 — vendor_candidates.business_registration_number
```sql
ALTER TABLE vendor_candidates ADD COLUMN business_registration_number TEXT;
```
- NULL 허용, 기존 데이터 영향 없음

### 변경 3 — vendor_brn_checks 컬럼 추가
```sql
ADD COLUMN brn_verified BOOLEAN GENERATED ALWAYS AS (status = 'active') STORED,
ADD COLUMN address_match BOOLEAN,
ADD COLUMN website_match BOOLEAN,
ADD COLUMN cross_source_count SMALLINT NOT NULL DEFAULT 0,
ADD COLUMN cross_validation_failed BOOLEAN GENERATED ALWAYS AS (...) STORED
```

### 변경 4 — ftc_telesales_registry 신규 테이블
공정위 통신판매업 신고 참조 데이터. BRN + 신고번호 UNIQUE. RLS 활성화.

## 리스크
- 모두 ADD (신규 컬럼/테이블) — DROP 없음, 롤백 쉬움
- GENERATED ALWAYS AS STORED: Postgres 12+ 지원 (Supabase 기본)
- Legal 자문 [PACAA-788](/PACAA/issues/PACAA-788) 동시 진행 중

## 요청
마이그레이션 적용 승인 시 이 이슈를 `done` 처리해 주세요.
