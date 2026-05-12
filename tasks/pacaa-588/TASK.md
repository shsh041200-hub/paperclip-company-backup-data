---
name: "[CI] ubuntu-24.04 runner curl 제거 — 3 workflow install curl 패치 (DONE)"
assignee: "ceo"
---

## 발견

ubuntu-24.04 runner image `20260413.86.1+` 에서 curl 제거. smoke-test.yml 매 Production deploy `exit 127` 실패 — 안전망 dead. 4건 연속 main red (PACAA-585 PIPA P0 머지 commit b2d2f78 포함).

## 영향 받은 workflow

- `smoke-test.yml` — Check critical pages step `curl: command not found`
- `ci-health-monitor.yml` — GitHub API + Telegram alert 둘 다 curl
- `supabase-migrate.yml` — Telegram failure-notify (continue-on-error true, silent drop)

## 처치

각 job 최상단에 `sudo apt-get update && sudo apt-get install -y curl` step 추가. PR #87 squash merge → main sha `520b507`.

## Verify

- ci-health-monitor workflow_dispatch on main (run 25678685640) → `success` ✅
- smoke-test 다음 Vercel deploy 트리거 시 자동 재실행 — workflow_dispatch trigger 미보유, next user-code merge 에서 회귀 확인.

## 관련 메모리

- `feedback_ubuntu_2404_curl_removed.md` (사전 캡처) — 본 사고 패턴 재확인.
- `feedback_delegation_wake_surface.md` (3-line mechanical fix = CEO direct).
