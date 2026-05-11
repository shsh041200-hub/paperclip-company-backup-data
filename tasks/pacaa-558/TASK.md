---
name: "[CI P1 → CTO] supabase-migrate + smoke-test 4시간 silent red — PACAA-528 PR #64 회귀 의심"
assignee: "cto"
---

## 진단

PR #69 (PACAA-553, 머지 commit `b6d36bc7`) 직후 워크플로우 status 점검 시 발견.

### 적색 workflow

| Workflow | 마지막 success | 첫 failure | 적색 commit 수 | 가장 최근 commit |
| --- | --- | --- | --- | --- |
| `Supabase Migrate` (named) | `40e1aa85` 2026-05-11T02:27:48Z | — | — | 마지막 = success |
| `.github/workflows/supabase-migrate.yml` (file-named) | **없음** | `0dbb9429` 2026-05-11T03:25:49Z | 7 (전부 fail) | `b6d36bc7` |
| `smoke-test` | (history 안 success) | `e420d13f` 2026-05-11T03:18:49Z 이전 | 8+ | `b6d36bc7` (failed step: `Check critical pages`) |

### 회귀 시점 매칭

- `.github/workflows/supabase-migrate.yml` 첫 fail = 2026-05-11T03:25:49Z (`0dbb9429`)
- **PACAA-528 PR #64** 머지 시각 = 2026-05-11T03:25:47Z — **2초 차이**.
- PACAA-528 = "Supabase Migrate CI 실패 Telegram 알림 추가". 워크플로우 yaml 자체를 수정 → 새 워크플로우 ID 가 file-named 로 식별됨. jobs 배열이 `total_count: 0` (workflow validation 또는 trigger 미동작).
- → **PACAA-528 PR #64 가 telegram alert 추가하면서 workflow 자체를 break**. 결과: 텔레그램 알림도 안 가고, 마이그레이션도 안 돌고, board 도 모름.

### Silent 4시간

PACAA-526/PACAA-528 모두 status=done. 그러나 실제 워크플로우는 4h+ silent red 지속. **PACAA-526 의 "3일 silent red" 사고가 4시간 silent red 로 재발**.

### 추가 발견: smoke-test "Check critical pages" 실패

별 workflow `smoke-
