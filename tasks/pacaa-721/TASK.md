---
name: "[E7 stall_sweep] in_progress/blocked/backlog 이슈 stall 분류 + wake comment"
assignee: "ceo"
---

## 목적 (PACAA-167/169 Phase 1B E7)

매 6시간마다 회사 전체 in_progress/blocked/backlog 이슈 스캔 → unintended-stall 분류 (HEARTBEAT.md Phase 2 룰) → 발견 시 해당 이슈에 wake-comment 게시.

## 5 가드 (PACAA-166 v2 §4)

1. **Whitelist:** 본 routine은 'stall.detected' 이벤트만 발화. 다른 이벤트 키 금지.
2. **Rate limit:** 24h 내 동일 (issueId, classification) 재발화 차단.
3. **Idempotency key:** `stall.detected:{issueId}:{classification}:{YYYY-MM-DD}`.
4. **Audit log:** 본 routine 실행 결과는 `$AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl` 에 1줄씩 append (kind=E7, target=issueId, classification, allowed=true|false_with_reason).
5. **Kill switch:** routine PATCH `enabled: false` 또는 trigger PATCH `enabled: false` 즉시 차단.

## 실행 단계

1. GET /api/companies/{cid}/issues?status=in_progress,blocked,backlog 전수 fetch.
2. 각 이슈에 대해 분류:
   - `date-wait` — calendar/external date 대기 (legitimate).
   - `external-wait` — board UI / 외부 시스템 응답 대기 (legitimate, blockedByIssueIds=[] + 본문 명시).
   - `dependency-wait` — blockedByIssueIds 또는 pinned comment 명시 (legitimate).
   - `unintended-stall` — 위 3 외 + assigneeAgent heartbeat 미발사 (force wake 후보).
3. `unintended-stall` 발견 시 본인 (CEO) 이슈에 wake-comment 게시: `[wake-event] E7 stall.detected: PACAA-XXX <classification> at <IS
