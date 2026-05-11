---
name: "[CTO 인프라 P0] Supabase Migrate 워크플로우 3일 연속 실패 — schema_migrations 드리프트, PR #59 prod 미반영"
assignee: "cto"
---

## 발견

PACAA-515 PR #59 머지 (`35004752`, 01:56:17Z) 직후 `Supabase Migrate` 워크플로우 run `25646302599` 실패:

```
Remote migration versions not found in local migrations directory.
Make sure your local git repo is up-to-date. If the error persists, try repairing the migration history table:
supabase migration repair --status reverted 20260508
```

## 라이브 cross-check

GitHub Actions 워크플로우 `Supabase Migrate` (id=263367427) 히스토리 (최근 10건) — **2026-05-08T00:54:22Z 의 success 이후 모두 failure** (3일 연속):

| 시각 | sha | 메시지 |
|---|---|---|
| 2026-05-11T01:56:20Z | 35004752 | feat(PACAA-515): vendor evidence schema (#59) |
| 2026-05-10T09:24:32Z | c7622103 | fix(PACAA-466): DROP quote_requests schema |
| 2026-05-09T17:19:22Z | 3249c4ca | Merge PR #25 from feat/db-quote-requests-PACAA-354 |
| 2026-05-09T08:00:52Z | 2b880829 | fix(migrations): resolve duplicate version prefix 20260508 (PACAA-382) (#29) |
| 2026-05-08T15:34:21Z | dc699165 | PIPA 처리방침 개정 (#23) |
| 2026-05-08T00:54:22Z | 682a498c | **success** — feat(db): keyword_pages DB 전환 (#18, PACAA-288) |

→ PACAA-382 의 "fix" PR #29 (`2b880829`) 머지 직후부터 워크플로우 빨갛음. PACAA-382 는 done 으로 닫혔지만 실 fix 미완료. 이후 3일간 누구도 워크플로우 상태 모니터링 안 함 (systemic 사각).

## 영향

-
