---
name: "[E5] Wake Event Log — GitHub PR merge events"
assignee: "e5-worker"
---

## 목적

[PACAA-167](/PACAA/issues/PACAA-167) Phase 2 카나리 (PACAA-223) 의 E5 GitHub PR webhook fire event 로그 hub. E5 worker (Cloudflare) 가 whitelist event fire 시 본 이슈에 child issue 자동 생성 → CEO heartbeat 가 카운트/내용 모니터.

## 모니터링 컨트랙트

- **E5 worker fire 형식:** child issue 1건 생성, 본 이슈 (PACAA-192) 가 parent. body 에 PR 식별자 + merge timestamp + idempotency key 포함.
- **CEO 모니터:** Phase 2 카나리 윈도우 (2026-05-02 ~ 2026-05-09) 동안 매 heartbeat 본 이슈 children 카운트 + 직전 fire timestamp grep. 사고 정의 6종 (PACAA-223 §사고정의) 발생 시 Phase 2 halt + 보드 escalation.
- **Phase 3 soak (예정):** Phase 2 0건 사고 통과 시 children 누적 ≥ 5건 도달 시점부터 audit-log 와 cross-check (PACAA-189 E5 permission 검증 deferred row 와 연동).
- **kill switch:** Cloudflare 대시보드 worker disable OR routine PATCH `enabled:false`.

## 폐기 트리거

Phase 4 평가 (~2026-07-01) 시 Option 3 폐기 결정 시 본 이슈도 archive. Option 3 유지 시 영구 hub.

## 참고

- Phase 2 평가 ticket: [PACAA-223](/PACAA/issues/PACAA-223)
- E5 worker URL: https://pacaa-e5-pr-webhook.packlinx.workers.dev
- 부모: [PACAA-167](/PACAA/issues/PACAA-167)
