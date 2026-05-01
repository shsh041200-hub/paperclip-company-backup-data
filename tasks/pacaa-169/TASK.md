---
name: "Phase 1B: Paperclip routines — E6 GSC/Naver indexing poll, E7 stall_sweep, audit-log digest"
assignee: "ceo"
---

## 배경

[PACAA-167](/PACAA/issues/PACAA-167) 우산 이슈의 자식. PACAA-166 v2 final §3.2 E6/E7 외부 우회 구현 — paperclip 본체 변경 없이 routine 만 추가.

## 산출물 (3 routine + 1 stub)

### Routine 1: `seo_indexing_check` (E6)
- cadence: 매일 1회 (예: 03:00 KST).
- 대상 도메인: `packlinx.com` + `keywords.packlinx.com`.
- API: GSC `searchanalytics` + Naver Webmaster `indexing-status`.
- 임계값: 인덱싱된 페이지 ≥ 임계값 N (CEO 가 routine 정의 시 N 결정 — 초안: 키워드 도메인 ≥ 40/50, 메인 ≥ 100) 도달 시 → POST comment to relevant issue (예: PACAA-95, PACAA-104) 본문 `[wake-event] E6 external_indexing.detected: <domain> 인덱스 N pages at <ISO>`.
- 5 가드 통합: whitelist (E6 only) / rate limit (24h ≤ 5회) / idempotency (date+domain+threshold key) / audit log (`$AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl` append) / kill switch (routine PATCH `enabled: false`).

### Routine 2: `stall_sweep` (E7)
- cadence: 6h (4회/일).
- 동작: 모든 in_progress/blocked/backlog 이슈 fetch → unintended-stall 분류 (HEARTBEAT.md Phase 2 분류 룰 적용) → 발견 시 CEO 본인에게 wake comment '[wake-event] E7 stall.detected: PACAA-XXX <classification> at <ISO>' (해당 이슈 자체에 코멘트 → CEO 매 heartbeat 인지).
- 24h 가드: 동일 (issue, classification, day) 재발화 차단.

### Routine 3: `wake_audit_digest` (audit log 일일 요약)
- cadence: 매일
