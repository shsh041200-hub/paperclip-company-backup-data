---
name: "P1.2 스키마 CTO sign-off — packaging_categories + vendor_candidates"
assignee: "cto"
---

## 목적

P1.2 vendor target list 수집 전에 신규 테이블 2개에 대한 CTO sign-off가 필요합니다.

## 검토 요청 파일

`plans/migration_p1_2_v1.sql` (Backend Engineer workspace)

## 변경 요약

### 1. `packaging_categories` (신규)
- P1.1 `category_denominators.category_key` (text)의 정규화 참조 테이블
- 8개 카테고리 seed — P1.1 DB 실측값과 key 일치 확인
- 모든 P1.2+ 테이블이 이 테이블의 uuid FK를 사용
- `category_denominators`는 **무변경** (text key 유지)

### 2. `vendor_candidates` (신규)
- P1.2 raw 수집 레코드 저장
- 필수 필드: `source`, `source_attribution jsonb` (SOUL.md 필수 조건)
- `dedup_status` (raw → P1.3이 clean/duplicate/merged로 관리)
- soft delete (`deleted_at`) — raw 레코드 원본 영구 보존
- `canonical_id` self-ref FK — P1.3 duplicate 체인

### 인덱스
- `(category_id, source, source_id)` UNIQUE (idempotency)
- `(dedup_status)`, `(category_id, dedup_status)` (P1.3 pipeline + coverage 계산)
- `(business_name)` (P1.3 dedup heuristics)

### CTO 검토 포인트
1. packaging_categories seed의 KSIC 코드 — P1.1 KOSIS API 결과와 일치 여부
2. vendor_candidates 인덱스 전략 — 특히 dedup_status + category_id composite
3. dedup_status CHECK constraint 값 세트 — P1.3 pipeline과 호환 여부 확인
4. RLS 활성화 필요 여부 — 현재 두 테이블 모두 RLS ENABLE
5. canonical_id ON DELETE SET NULL — duplicate 체인 정합성 검토

## 롤백 계획

```sql
BEGIN;
DROP TABLE vendor_can
