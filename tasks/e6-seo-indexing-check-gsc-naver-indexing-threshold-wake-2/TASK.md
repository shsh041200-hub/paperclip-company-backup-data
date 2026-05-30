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
- 매일 GSC 조회 + audit log 기록은 유지.
- packlinx.com가 임계값을 충족하더라도 wake-event comment를 발송하지 않음 (idempotency 키 소모하지 않음).
- audit log에 status: suppressed_permanent_met 기록 (측정값 + 사유 포함).
- suppression 해제 조건: packlinx.com 인덱싱이 100 미만으로 하락 감지 시 → 즉시 wake-event 발송 재개 + audit log에 suppression_lifted: true 기록.
- keywords.packlinx.com은 이 suppression에 영향받지 않음 (별도 임계값 ≥ 40 달성 시 정상 wake-event 발송).

### 🆕 Naver Webmaster 연동 (PACAA-732)

#### env 변수 (canonical)
아래 두 환경변수를 adapterConfig.env에 설정해야 Naver 인덱싱 측정이 활성화됨.
- `NAVER_SEARCHADVISOR_API_KEY` — Naver Search Advisor 공개키 (사이트 대시보드 > API 키 관리 > 공개키)
- `NAVER_SEARCHADVISOR_API_SECRET` — Naver Search Advisor 비밀키 (동일 화면 > 비밀키)

#### Naver indexing-status 호출 로직 (실행 순서)
1. 실행 시작 시 `NAVER_SEARCHADVISOR_API_KEY` / `NAVER_SEARCHADVISOR_API_SECRET` 존재 여부 확인.
2. **자격증명 누락 시 (kill switch 자동화)**:
   - audit log (`$AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl`)에 다음 구조로 append:
     ```json
     {"ts": "<ISO>", "event": "naver_skipped", "reason": "missing_creds", "domains": ["packlinx.com", "keywords.packlinx.com"]}
     ```
   - GSC만 진행. Naver 구간 완전 건너뜀. routine 중단하지 않음.
3. **자격증명 존재 시 (Naver API 호출)**:
   - HMAC-SHA256 서명 생성:
     - message = `{timestamp}\n{NAVER_SEARCHADVISOR_API_KEY}` (timestamp = Unix epoch 밀리초)
     - signature = base64(HMAC-SHA256(NAVER_SEARCHADVISOR_API_SECRET, message))
   - 각 도메인에 대해 GET 요청:
     ```
     GET https://api.searchadvisor.naver.com/console/openapi/v1/site-dashboard/indexed?site_url=<도메인>
     Headers:
       X-Naver-Client-Id: {NAVER_SEARCHADVISOR_API_KEY}
       X-Naver-Client-Sign: {signature}
       X-Naver-Timestamp: {timestamp}
     ```
   - 응답 `data.indexedCount` 값을 GSC 측정값과 함께 audit log에 기록:
     ```json
     {"ts": "<ISO>", "event": "naver_indexing_check", "domain": "<domain>", "indexed_pages": <N>, "source": "naver_webmaster"}
     ```
   - API 오류(4xx/5xx) 시: audit log에 `{"event": "naver_api_error", "status": <code>, "domain": "<domain>"}` 기록 후 해당 도메인 건너뜀. routine 중단하지 않음.
4. **임계값 적용**: Naver 인덱싱은 별도 임계값 없음 — 측정·기록만. GSC 임계값 wake-event 로직은 기존 동작 유지.
5. **자격증명 입력 후 첫 실행 확인**: audit log에 `naver_skipped` 없이 `naver_indexing_check` 기록 시 Naver 연동 정상.
