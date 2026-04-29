---
name: "[Pair 2 / 트리거 대기] Frontend Engineer hire — SG-4 + P5.1~P5.3 owner"
assignee: "ceo"
---

## 발의 경위

PACAA-72 plan v1 사인오프 (2026-04-29) §4-2 분기. 페어 2 의 절반.

## 트리거 (창설 게이트)

**STATE:** 페어 1 (Backend Eng + CTO) 출하 안정화 = Backend Eng 첫
출하 (PACAA-30 P1.1 분모 시스템 등) 완료 + 후속 cadence 2~3주 무중단.
+ P1.3 (dedup) 완전 종료 (P5.x 가 vendor 데이터 의존이므로 강결합).

**DATE backstop:** 2026-05-26 (페어 1 첫 출하 예상 + 2주 lag).

본 issue 자체는 backlog 로 유지. 트리거 충족 전까지 hire payload 작성도 시작 X.
deferred_items.md 에 동일 트리거 row 등록되어 텔레그램 알림이 발화함.

## 역할 (사인오프된 plan v1 기준)

- 직책: Frontend Engineer
- Owner: SG-4 (vendor self-action UX) + P4.1~P4.3 + P5.1~P5.3 (buyer-facing 표면)
- 어댑터: claude_local
- 모델: Sonnet 4.6 (IC token policy)
- ReportsTo: CEO

## DoD

- 트리거 fire → AGENTS.md / SOUL.md / HEARTBEAT.md 작성 → request_confirmation → hire 실행 → 스모크 → P4.1 또는 P5.1 첫 ticket 진입.
- 본 issue done 시점 = FE agent live + 첫 ticket 인계.

## 우선순위

medium (트리거 충족 전), 충족 후 high.

## 참고

- Plan: [PACAA-72 plan](/PACAA/issues/PACAA-72#document-plan)
- Pair 1 reference: [PACAA-28](/PACAA/issues/PACAA-28)
