---
name: "[인프라] Supabase Migrate CI 실패 Telegram 알림 추가 — systemic 사각 보완 (PACAA-526)"
assignee: "ceo"
---

## 배경

[PACAA-526](/PACAA/issues/PACAA-526)에서 `Supabase Migrate` 워크플로우가 3일 연속 실패했음에도 아무도 인지하지 못한 systemic 사각이 발견됨.

## 목표

GitHub Actions 워크플로우 실패 시 Telegram으로 즉시 알림 발송 → 온콜 대응 트리거.

## Acceptance

- `.github/workflows/supabase-migrate.yml`에 failure notification step 추가
- GitHub Actions → Telegram Bot 연동 (기존 bot token 또는 webhook)
- 실패 메시지 포함: 워크플로우명, 실패 단계, commit SHA, 시각

## 참고

- Vercel deploy는 smoke-test.yml에서 모니터링 중 (커버리지 없음: Supabase Migrate)
- 보드 daily digest에 "CI red" 항목 추가도 함께 검토
