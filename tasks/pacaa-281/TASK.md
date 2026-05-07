---
name: "[Idle-improvement #2-impl] vendor 비교 테이블 — implementation"
assignee: "frontend-engineer"
---

## 배경
PACAA-265 spec accept (CEO 검토 9894f603 — 2026-05-07). 이 이슈에서 구현.

## Spec 핵심
- 카테고리/벤더 페이지에 "비교 추가" 버튼
- 하단 비교 카트 드로어 (max 3 vendor)
- localStorage 기반 (DB schema 변경 없음)
- 텍스트/배지 비교 테이블 (18 필드)
- 모바일/데스크톱 모두
- 자세한 spec: PACAA-265 코멘트

## Acceptance
- [ ] PR 머지 + 라이브
- [ ] mobile 375px / desktop 1440px 둘 다 시각 검증
- [ ] localStorage persistence 동작 (페이지 이동 후 카트 유지)
- [ ] 머지 후 즉시 CEO escalation 코멘트 (in_review passive 금지 — feedback_subagent_immediate_escalation 룰)

## 의존성
없음 — spec 확정.
