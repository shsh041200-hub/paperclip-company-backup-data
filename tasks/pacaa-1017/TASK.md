---
name: "PACAA-1016 후속 — Tier-2 token-saving levers"
assignee: "ceo"
---

PACAA-1016 옵션 A 즉시 실행분(L1/L2/L3/L5) 완료 후 Tier-2 후속.

## Checklist (각 항목 작은 이슈로 split 가능)

- [ ] **L4 Sub-agent context 최소화** — Agent invoke prompt 에 'do not re-read SOUL/HEARTBEAT' 명시 가능성 검토 + CEO discipline
- [ ] **L6 Comment thread pruning policy** — Phase 2 stall scan 시 thread body 안 보고 status/title 만, ESCALATION grep 시에만 body
- [ ] **L7 Wake interval night-mode** — 한국 02:00-08:00 만 hb 30min, interaction wake 는 즉시 (PACAA-1016 권장하나 별도 검증)
- [ ] **L8 Cache-friendly ordering** — harness 팀에 prompt prefix 정적/동적 분리 가능성 문의, MEMORY.md update 빈도가 캐시 invalidation 되는지 확인
- [ ] **L9 Routine consolidation** — daily-digest, idle-improvement, stall-scan 등 별도 wake → consolidate 가능성 audit
- [ ] **L4-MEM archive** — MEMORY.md 의 fully-internalized historical entries 를 archived_memory/ 로 이동 (recall 비활성)
- [ ] **Quick-exit marker file** — `runs/last-phase5-rotation.txt` timestamp marker 도입, Journal grep 의존 제거 (PACAA-1016 L3 의 follow-up)
- [ ] **Token telemetry** — harness 가 input/output token 을 run record 에 저장하는지 확인. 있으면 wake 당 baseline 측정

## 의존성

별도 interaction 6d1e0bcf (CEO effort=medium + hb 900→1800) 결정과 무관 — 그쪽은 model/cadence 축, 본 child 는 protocol/data hygiene 축.

## 우선순위

측정 (token telemetry)
