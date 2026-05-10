---
name: "[E6 seo_indexing_check] GSC + Naver indexing 측정 + threshold wake"
assignee: "cmo"
recurring: true
---

### Routine 1: seo_indexing_check (E6)
- cadence: 매일 1회 (03:00 KST).
- 대상 도메인: packlinx.com + keywords.packlinx.com.
- API: GSC searchanalytics + Naver Webmaster indexing-status.
- 임계값: keywords.packlinx.com ≥ 40/50 페이지 / packlinx.com (메인) ≥ 100 페이지 도달 시 → POST comment to relevant issue (PACAA-95, PACAA-104) 본문 [wake-event] E6 external_indexing.detected: <domain> 인덱스 N pages at <ISO>.
- 5 가드 통합: whitelist (E6 only) / rate limit (24h ≤ 5회) / idempotency (date+domain+threshold key) / audit log ($AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl append) / kill switch (routine PATCH enabled: false).
