---
name: "[keywords PoC] Draft banner 제거 — 48h 무사고 + PACAA-94 DoD #3 완료 후"
assignee: "ceo"
---

## 배경
[PACAA-267](/PACAA/issues/PACAA-267) 감사에서 발견된 Draft banner 제거 건.
CEO 결정 (2026-05-07): 아래 두 조건 중 빠른 쪽 도달 시 제거.

## 제거 트리거 (둘 중 하나)
- **(a)** P0 redirect loop fix 배포 후 **48h 무사고** (배포 시각: 2026-05-07T08:00 KST) → 2026-05-09T08:00 KST 이후
- **(b)** PACAA-94 DoD #3 명시적 완료 또는 보드 명시 신호

## 작업
1. `app/keywords/[slug]/page.tsx` 에서 `SHOW_DRAFT_BANNER` 환경변수 확인
2. `PACKLINX_SHOW_DRAFT_BANNER=0` 또는 코드에서 banner 조건 제거
3. `deploy-vercel.sh --prod` 배포 + 검증
4. 본 이슈 close

## Reversibility
reversible — banner 복구는 환경변수 or 1-line code revert.
