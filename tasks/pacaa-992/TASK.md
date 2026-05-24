---
name: "[CTO] PR #177 코드 리뷰 — companies.vendor_model migration"
assignee: "cto"
---

## 요청

[PACAA-986](/PACAA/issues/PACAA-986) 후속 — Legal Counsel PIPA sign-off 완료.

PR #177 코드 리뷰 요청: https://github.com/shsh041200-hub/pkging-platform/pull/177

## 검토 항목

1. `supabase/migrations/20260524001_vendor_model_column.sql`
   - `companies.vendor_model` nullable TEXT CHECK (found | not_found | exempt)
   - `companies.vendor_model_source` nullable TEXT CHECK (name_match_provisional | brn_verified | self_reported)
   - COMMENT ON COLUMN PIPA 경고 포함
2. `scripts/runs/pacaa986_backfill_vendor_model.sql`
   - DISTINCT ON(vendor_id) ORDER BY checked_at DESC 멱등성
   - WHERE vendor_model IS NULL 조건 확인
3. `search_companies_korean` RPC — select * 반환 시 vendor_model 외부 노출 여부 검증

## Legal Counsel 자문 결론 ([PACAA-989](/PACAA/issues/PACAA-989))

- PR #177 merge 가능 (처리방침 업데이트는 [PACAA-990](/PACAA/issues/PACAA-990)으로 트래킹)
- FE 노출 전 별도 자문 필수 (표시광고법 §3)

## 완료 기준

- PR approve + merge (또는 변경 요청 시 comment)
- merge 후 `node scripts/db-migrate.mjs` 적용 + backfill 실행 승인
