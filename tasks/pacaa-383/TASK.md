---
name: "[PACAA-322] quote_requests 파기 잡 — pg_cron vs Edge Function 결정 + 등록"
assignee: "cto"
---

## 목적

[PACAA-354](/PACAA/issues/PACAA-354) Phase 1 마이그레이션에서 분리된 잔여 항목. PIPA §39-3 (수집·이용 동의 만료 후 30일 이내 파기) 의무 충족을 위한 일일 파기 잡 등록.

## 배경

`quote_requests` + `quote_requests_purge_log` 테이블은 [PACAA-354](/PACAA/issues/PACAA-354) 에서 prod Supabase 에 생성 완료 ([적용 내역 코멘트](/PACAA/issues/PACAA-354#comment-9bea49fb-7a55-4b43-8f2b-1318f4ae0701)). 단, [PACAA-322](/PACAA/issues/PACAA-322) plan v2 §1 의 `pg_cron` 잡 등록은 본 Supabase 프로젝트에 `pg_cron` extension 이 비활성이라 미적용 — CTO 결정 필요.

## 옵션

**옵션 1 — `CREATE EXTENSION pg_cron`**

- 비용: $0 (이미 활성화 가능, Supabase Pro 이상 또는 self-hosted 모두 지원).
- 이미 작성된 SQL 그대로 사용 가능:
  ```sql
  SELECT cron.schedule(
    'purge_expired_quote_requests',
    '0 18 * * *',  -- 03:00 KST
    $$
      WITH deleted AS (
        DELETE FROM quote_requests WHERE expires_at < now() RETURNING id
      )
      INSERT INTO quote_requests_purge_log (purged_count) SELECT count(*) FROM deleted;
    $$
  );
  ```
- 장점: DB 내부 완결, 외부 의존 없음, 모니터링은 `cron.job_run_details`.
- 단점: extension 활성화는 DB 차원 변경 (다른 잡에도 영향), 실패 알림 별도 필요.

**옵션 2 — Supabase Edge Function + scheduled trigger**

- 비용: Edge Function 호출 1회/일 — Supabase Free tier 한도 내.
- 새 함수 (e.g., `purge-expired-quote-requests`) + Vercel/Clou
