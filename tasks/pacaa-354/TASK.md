---
name: "[PACAA-322] DB migration — quote_requests 테이블 + 파기 로그"
assignee: "cto"
---

## 목적

[PACAA-322](/PACAA/issues/PACAA-322) plan v2 Phase 1. quote_requests 테이블 신설 + 자동 파기 잡 기반 마련.

## 작업

1. **마이그레이션 파일 작성:** `supabase/migrations/20260509_quote_requests.sql`
   - `quote_requests` 테이블 (plan §1 스키마 그대로)
   - 동의 컬럼 2개 분리: `consent_collection` + `consent_third_party` (각 BOOLEAN NOT NULL + *_at TIMESTAMPTZ NOT NULL)
   - `expires_at` GENERATED AS (consent_collection_at + INTERVAL '1 year') STORED
   - 인덱스: created_at DESC, status, expires_at
   - RLS: public INSERT, service role SELECT/UPDATE
   - `quote_requests_purge_log` 파기 로그 테이블 (id, purged_count, purged_at)
2. **pg_cron 파기 잡 등록** (또는 Supabase Edge Function cron): 매일 03:00 KST — expires_at < now() DELETE + 로그 INSERT
3. **마이그레이션 적용:** `node scripts/db-migrate.mjs`
4. **확인:** Supabase 대시보드 또는 psql에서 테이블 존재 + RLS 정책 확인

> **파일명 변경 이력:** `20260508_quote_requests.sql` → `20260509_quote_requests.sql` (CTO 경고: 20260508 버전 schema_migrations 중복)

## Plan 참조

[PACAA-322 Plan §1 데이터 모델](/PACAA/issues/PACAA-322#document-plan)

## Acceptance
- [x] 마이그레이션 파일 생성 (20260509_quote_requests.sql)
- [ ] quote_requests 테이블 생성 확인
- [ ] consent_collection + consent_third_party 컬럼 분리 확인
- [ ] expires_at 자동 계산 확인
- [ ] 파기 잡 등록 확인
