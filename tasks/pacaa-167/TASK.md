---
name: "이벤트 기반 wake 시스템 구축 (Option 3) — 실행 (Phase 1~4)"
assignee: "ceo"
---

## 배경

[PACAA-166](/PACAA/issues/PACAA-166) 분석 결과 보드 사인오프 완료 (interaction f4f5c7ea, 2026-05-01 09:36 KST). Option 3 (외부 우회) + Phase 4 A/B/C 임계값 + PACAA-146 paradigm 관계 진단 모두 채택.

## 산출물

PACAA-166 v2 final plan §6~9 의 Phase 1~4 실행을 본 이슈가 추적.

- **Phase 1 (~2주):** 외부 worker (E5 GitHub PR webhook) + paperclip routines (E6 GSC/Naver poll, E7 stall_sweep) + 5 가드 외부 강제.
- **Phase 2 (1주 카나리):** E5 만 활성화. 사고 0 검증 시 E6/E7 순차 활성화.
- **Phase 3 (~1.5개월 soak):** A/B/C 데이터 수집. 월간 리포트 routine.
- **Phase 4 (평가):** §10.2 게이트 매칭 → Option 3 유지 vs Option 1 재고 결정.

## DoD (umbrella)

- Phase 1A (외부 worker, Backend Eng) + Phase 1B (paperclip routines, CEO) 자식 이슈 발의 + 둘 다 done.
- Phase 2 카나리 자식 이슈 (Phase 1 완료 시 event-driven 발의).
- Phase 3 soak monitoring routine 등록 + 매월 A/B/C 리포트 생성.
- Phase 4 평가 child issue (Phase 3 종료 시 발의, deferred_items.md row 와 연동).

## 트리거 / 일정

- Phase 1A·1B 즉시 시작 (parallel).
- Phase 2 = Phase 1A + 1B 둘 다 done 트리거 (event-driven).
- Phase 3 = Phase 2 카나리 1주 사고 0 트리거.
- Phase 4 = Phase 3 시작 + 60일 cron OR catastrophic 사고 1건 즉시.

## 안전성 가드 (PACAA-166 v2 §4)

5 가드 외부 시스템에 강제 적용:
1. Whitelist (worker/routine 코드에 hard-coded 7 이벤트 키)
2. Rate limit (24h ≤ 5회, kind/source/target 별)
3. Idem
