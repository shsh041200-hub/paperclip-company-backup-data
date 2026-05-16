---
name: "[wake_audit_digest] 직전 24h wake event audit log → board digest 첨부"
assignee: "ceo"
---

## 목적 (PACAA-167/169 Phase 1B Routine 3)

매일 09:00 KST (PACAA-53 Daily Board Digest 와 동시) 직전 24h `runs/wake_audit-YYYY-MM-DD.jsonl` 요약 → PACAA-53 board digest issue 에 코멘트 자동 첨부.

## 5 가드
1. **Whitelist:** 본 routine 은 wake event 를 발화하지 않음 (조회 + 코멘트만). 이벤트 키 발화 0.
2. **Rate limit:** N/A (비 발화 routine).
3. **Idempotency:** `wake_audit_digest:{YYYY-MM-DD}` — 동일 일자 재실행 시 코멘트 1회만.
4. **Audit log:** 본 routine 자체는 audit log 의 *consumer* — 자체 행위는 별도 기록 불필요.
5. **Kill switch:** routine PATCH `enabled: false`.

## 실행 단계
1. 어제 일자 KST = `YYYY-MM-DD` 결정. `$AGENT_HOME/runs/wake_audit-YYYY-MM-DD.jsonl` 읽기.
2. 파일 없으면 `wake events: 0 (file missing)` — 정상 (그 날 fire 0건).
3. line-by-line JSON parse → kind 별 카운트 (E1/E5/E6/E7/etc) + reject 사유별 카운트.
4. PACAA-53 (Daily Board Digest) 의 *오늘 spawn 된 issue* 식별 (lastTriggeredAt 기반) → 그 이슈에 코멘트 게시:
   `[wake-audit] {YYYY-MM-DD}: E1=N건 / E5=N건 / E6=N건 / E7=N건 / reject=N건 (rate=R, idempotent=I, whitelist=W)`
5. 본 spawned issue 결과 코멘트 + done.

## DoD
- audit log 파싱 성공 (또는 파일 없음 정상 처리).
- board digest issue 에 코멘트 게시.
- 본 spawned issue done.

## 출처
- 부모 routine: PACAA-169 Phase 1B Routine 3.
- 우산: PACAA-167.
