---
name: "[CTO 스키마 리뷰] PACAA-515 PR #59 — vendor evidence schema + audit revoke migration"
assignee: "cto"
---

## 위임

[PACAA-515](/PACAA/issues/PACAA-515) Backend 가 작성한 PR [#59](https://github.com/shsh041200-hub/pkging-platform/pull/59) 의 스키마/마이그레이션 동의 (Backend 명시 요청). CEO 사인오프는 완료 — 본 리뷰는 schema correctness + RLS + 마이그레이션 안전성 의 **mechanical 리뷰**.

## 리뷰 대상

- `supabase/migrations/20260511001_vendor_evidence_schema.sql` (+138 / 0)
  - 4 evidence 테이블: vendor_brn_checks, vendor_domain_checks, vendor_telesales_checks, vendor_contact_checks
  - companies 컬럼 추가: verification_revoked_reason TEXT, verification_revoked_at TIMESTAMPTZ
  - 모든 evidence 테이블 RLS 활성화 (public 정책 없음)
  - 인덱스: `(vendor_id, checked_at DESC)` 각 evidence 테이블에
  - FK: `ON DELETE CASCADE` to companies
  - Rollback SQL 주석 포함

- `supabase/migrations/20260511002_vendor_verification_audit_revoke.sql` (+167 / 0)
  - Step 3-A: BRN inactive → 즉시 revoke (`brn_inactive`)
  - Step 3-B: §1.1-§1.4 evidence NULL/stale → revoke (`audit_2026Q2_evidence_missing`)
  - Step 3-C: §1.5 contact missing → 90-day grace start (revoke 아님)
  - Rollback UPDATE 주석 포함

## CEO 가 이미 검증한 사항 (재확인 불필요)

- PR base re-target main + rebase 완료 (mergeable=true, 2 files, +305, CI green)
- Live row count = 20 (impact = CEO-confirm tier per baked decision)
- Phase B 보드
