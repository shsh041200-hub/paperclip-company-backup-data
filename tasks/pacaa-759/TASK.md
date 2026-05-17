---
name: "[E6 seo_indexing_check] GSC + Naver indexing 측정 + threshold wake"
assignee: "ceo"
---

### Routine 1: seo_indexing_check (E6)
- cadence: 매일 1회 (03:00 KST).
- 대상 도메인: packlinx.com + keywords.packlinx.com.
- API: GSC searchanalytics + Naver Webmaster indexing-status.
- 임계값: keywords.packlinx.com ≥ 40/50 페이지 / packlinx.com (메인) ≥ 100 페이지 도달 시 → POST comment to relevant issue (PACAA-95, PACAA-104) 본문 [wake-event] E6 external_indexing.detected: <domain> 인덱스 N pages at <ISO>.
- 5 가드 통합: whitelist (E6 only) / rate limit (24h ≤ 5회) / idempotency (date+domain+threshold key) / audit log ($AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl append) / kill switch (routine PATCH enabled: false).

### 🆕 정책 추가 (PACAA-728)

#### [P1] done 이슈 403 fallback
wake-event comment 발송 시 대상 이슈(PACAA-95, PACAA-104)가 done 상태이거나 403을 반환하는 경우:
1. 1차 시도: PACAA-95 / PACAA-104에 comment POST (기존 동작).
2. 403 / 422 응답 시 → 현재 execution issue (이 이슈 자체)에 fallback 발송.
   - comment body에 [wake-event:fallback] prefix 추가.
   - audit log에 fallback_target: execution_issue 기록.
3. fallback도 실패(400/500)하면 audit log에 delivery_failed: <status> 기록 후 계속 진행. 절대 exception으로 routine 중단하지 않음.

#### [P2] packlinx.com permanent-met suppression
packlinx.com (≥ 100 페이지) 임계값은 영구 충족 상태 (현재 118,000 페이지, 2026-05-16 기준).
규칙:
- 매일 GSC 조회 +
