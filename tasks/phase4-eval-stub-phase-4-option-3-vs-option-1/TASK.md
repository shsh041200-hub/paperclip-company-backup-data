---
name: "[phase4_eval STUB] Phase 4 평가 — Option 3 유지 vs Option 1 재고"
assignee: "ceo"
recurring: true
---

## STUB ROUTINE — 트리거 미설정

Phase 3 시작 (= Phase 2 카나리 1주 사고 0 트리거 후 routine 본격 활성화 + soak 시작) 시점에 본 routine 의 trigger 를 추가하여 Phase 3 시작 + 60일 단발 cron 으로 fire.

## 목적 (PACAA-167/169 Phase 1B Routine 4 stub)

Phase 3 (~1.5개월 soak) 종료 시점에 PACAA-166 v2 §10.2 게이트 매칭 → Option 3 (외부 우회) 유지 vs Option 1 (paperclip 본체 변경) 재고 결정.

## fire 시 실행 단계
1. 직전 60일 audit log 전체 fetch + 사고 카운트 + A/B/C 임계값 검증 (PACAA-166 v2 §10.2 게이트 매칭).
2. PACAA-167 우산 이슈에 코멘트: `[wake-event] phase4_eval.due: Phase 3 종료 — A=N건/B=N건/C=N건 + 사고 N건 → <Option 3 유지 / Option 1 재고> 권고.`
3. CEO 가 본 코멘트로 wake → 정식 평가 child issue 발의 + 보드 사인오프.

## 트리거 등록 가이드
- Phase 3 시작일 = T. cron = `0 9 (T+60일).day (T+60일).month *` Asia/Seoul. 단발 = catchUpPolicy=skip_missed + concurrencyPolicy=skip_if_active.
- 별도 catastrophic 사고 1건 즉시 트리거: 본 routine 외, audit log 또는 별도 로그에서 P0 사고 발견 시 CEO 직접 본 routine 의 spawned issue 1건을 manual POST 하여 평가 가속.

## 5 가드
1. Whitelist: 본 routine 은 'phase4_eval.due' 이벤트만.
2. Rate limit: 단발이라 N/A.
3. Idempotency: `phase4_eval:{YYYY-MM-DD}`.
4. Audit log: append.
5. Kill switch: routine PATCH `enabled: false`.

## 출처
- 부모 routine: PACAA-169 Phase 1B Routine 4 stub.
- 우산: PACAA-167.
- 연동: deferred_items.md row (Phase 4 평가).
