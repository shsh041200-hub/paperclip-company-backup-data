---
name: "[PACAA-1016 Batch B] Tier-2 token-savings levers (1주 baseline 후 평가)"
assignee: "ceo"
---

PACAA-1016 Batch B (Tier-2) — Token-savings 후속.

직전 Batch A (L1+L2+L3+L5) 는 본 hb 에 즉시 적용 완료. 본 issue 는
research-v0.md Tier-2 5개 lever 를 1주 baseline 측정 후 평가/실행.

## Tier-2 levers
- **L4. Sub-agent context 최소화** (-3K tok/invoke): CEO prompt 에
  "do not re-read SOUL/heartbeat" 명시 패턴 정착.
- **L6. Issue comment thread pruning**: Phase 2 stall scan 시 thread
  body 안 보고 status/title 만 사용 (ESCALATION grep 예외 유지).
- **L7. Wake interval 야간 완화**: 한국 02-08시 hb 15→30분. event
  trigger 즉시.
- **L8. Cache-friendly ordering**: MEMORY.md 정적/동적 분리, harness
  팀에 prefix matching 확인 요청.
- **L9. Routine consolidation**: paperclip routine list 점검, 중복/
  저-가치 제거.

## Schedule
- 1주 baseline (2026-05-25 ~ 2026-06-01): Batch A 단독 효과 측정
  (wake 횟수, Journal 누적, deferred items, ESCALATION grep miss).
- 2026-06-01 wake: 본 Tier-2 lever ROI 재평가, 우선순위 결정.

## Acceptance
- Batch A 1주 효과 정량 (wake 횟수 변화, 보드 reply latency 회귀
  없음, ESCALATION grep miss 없음) 보고.
- Tier-2 5개 중 ROI 상위 2-3개 선택 → 본 issue 안에 plan 으로 발의
  → 보드 confirm → 실행.

## Reference
$AGENT_HOME/plans/PACAA-1016/research-v0.md §2 Tier-2.
