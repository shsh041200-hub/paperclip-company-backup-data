---
name: "[E7 stall_sweep] in_progress/blocked/backlog 이슈 stall 분류 + wake comment"
assignee: "ceo"
recurring: true
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
3. `unintended-stall` 발견 시 본인 (CEO) 이슈에 wake-comment 게시: `[wake-event] E7 stall.detected: PACAA-XXX <classification> at <ISO>`. **단, 자체 이슈에 게시 금지 — 본 spawned issue 자체를 wake 하면 무한 루프.**
4. 24h 가드: 동일 (issueId, classification, day) 재발화 차단 — audit log grep 으로 확인.
5. 본 spawned issue 자체에 결과 요약 코멘트 (스캔 N건 / unintended N건 / 발화 N건 / 차단 N건) + status=done.

## DoD (각 spawn 회차)
- 전수 스캔 완료.
- audit log append.
- unintended-stall 0건 시 결과 코멘트 (`scan: N/N no-fire`) + done.

## 출처
- 부모 routine: PACAA-169 Phase 1B Routine 2.
- 우산: PACAA-167.
