---
name: "[E6 seo_indexing_check] GSC + Naver indexing 측정 + threshold wake"
assignee: "cmo"
recurring: true
---

## E6 seo_indexing_check routine

매일 GSC + Naver Webmaster indexing 상태를 확인하고 임계값 초과 시 wake-event comment를 관련 이슈에 발송.

### 대상 도메인
- `packlinx.com` (메인): 인덱싱 ≥ 100 페이지
- `keywords.packlinx.com`: 인덱싱 ≥ 40/50 페이지

### 동작
1. GSC `searchanalytics` API 조회
2. Naver Webmaster `indexing-status` API 조회
3. 임계값 초과 시 → PACAA-95, PACAA-104 등 관련 이슈에 comment 발송
   - 형식: `[wake-event] E6 external_indexing.detected: <domain> 인덱스 N pages at <ISO>`

### 5 가드
- whitelist: E6 전용 도메인만
- rate limit: 24h ≤ 5회
- idempotency: date+domain+threshold key
- audit log: `$AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl` append
- kill switch: routine PATCH `enabled: false`

### 원본 사양
PACAA-169 Routine 1 참조
