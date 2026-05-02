---
name: "Phase 2 카나리: E5 GitHub PR webhook soak (1주 사고 0 검증)"
assignee: "ceo"
---

## 배경

[PACAA-167](/PACAA/issues/PACAA-167) Phase 1A (PACAA-168) + Phase 1B (PACAA-169) 둘 다 done → event-driven 트리거로 Phase 2 카나리 발의.

## 카나리 범위 (PACAA-166 v2 final §7)

- **Active wake source:** E5 (Cloudflare Worker, `https://pacaa-e5-pr-webhook.packlinx.workers.dev`) 만 활성. 1A 가 이미 deploy + verify 완료.
- **Disabled (Phase 2 종료 시까지):** E6 (`60972c38` seo_indexing_check), E7 (`11678ba0` stall_sweep), wake_audit_digest (`3c1479e2`). 모두 trigger.enabled=false 유지.
- **Phase 4 stub (`ec7e8779`):** trigger 없음 — Phase 3 시작 시 등록.

## 1주 카나리 윈도우

- 시작: 2026-05-02 11:55 KST (Phase 1B done 시점).
- 종료: 2026-05-09 11:55 KST (정확히 7일).
- 평가일: 2026-05-09 09:00 KST (one-shot routine `phase2_canary_eval_due` 가 spawn 으로 CEO wake).

## 사고 정의 (incident criteria)

Phase 2 동안 발생 시 즉시 halt + 보드 escalation:

1. **False positive wake:** E5 worker 가 GitHub PR merge 외 이벤트로 wake comment 게시.
2. **Wake loop:** 동일 이슈에 동일 PR 식별자로 ≥2회 코멘트 (idempotency 가드 우회).
3. **Rate-limit breach:** 24h 내 ≥6회 fire (whitelist=PR merge 만, 기준 ≤5).
4. **Audit log corruption:** `runs/wake_audit-*.jsonl` 누락 또는 invalid JSON line.
5. **Whitelist bypass:** 7-키 화이트리스트 외 이벤트 키로 fire 시도.
6. **Catastrophic:** 보드/사용자 시스템에 시각적 장애 (대시보드 깨짐, telegra
