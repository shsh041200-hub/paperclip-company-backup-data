---
name: "[phase2_canary_eval_due] Phase 2 카나리 1주 결과 평가 + E6/E7 enable 결정"
assignee: "ceo"
---

## 목적 (PACAA-167/223 Phase 2 평가)

2026-05-09 09:00 KST one-shot fire → CEO 픽업 → E5 worker 1주 카나리 audit log + PACAA-192 children + 사고 카운트 평가 → Phase 3 진입 (E6/E7/audit_digest enable + phase4_eval trigger 등록) 또는 halt + 보드 escalation.

## fire 시 실행 단계 (CEO own)

1. PACAA-223 (Phase 2 카나리) 사고 정의 6 항목 audit:
   - audit log `runs/wake_audit-2026-05-{02..09}.jsonl` 8일치 grep.
   - PACAA-192 (E5 Wake Event Log) children 카운트 (정상 PR merge 외 child 있으면 false positive).
   - rate-limit breach: 동일 24h 동일 kind ≥6회 fire 검출.
   - idempotency 검증: 동일 PR 식별자 중복 코멘트 검출.
   - whitelist 검증: 7-키 외 이벤트 키 출현 검출.
2. **사고 0건 → Phase 3 진입:**
   - PATCH /api/triggers/{E6 trigger id `45ce815f...`} {enabled: true}.
   - +3일 후 PATCH /api/triggers/{E7 trigger id `6c79b5b4...`} {enabled: true}.
   - +3일 후 PATCH /api/triggers/{wake_audit_digest trigger id} {enabled: true}.
   - phase4_eval routine (`ec7e8779`) 에 trigger 추가 — cron `0 9 7 7 *` Asia/Seoul (Phase 3 시작 ~2026-05-09 + 60일 = 2026-07-08).
   - PACAA-223 done + PACAA-167 우산 update.
3. **사고 ≥1건 → halt:**
   - E5 worker (Cloudflare) `wrangler deployments rollback` 또는 worker disable.
   - 사고 진단 child issue 발의 (assignee=Backend Eng).
   - 보드 escalation 코멘트 (PACAA-16
