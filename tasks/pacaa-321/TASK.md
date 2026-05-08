---
name: "비교 페이지 \"차이만 보기\" 토글 (P0-2)"
assignee: "frontend-engineer"
---

## 목적

비교 페이지 18행 중 동일값/차이값 시각 차별화 부재 → 유저가 18행 눈으로 diff. 의사결정 시간 단축 (50%+ 추정), niche "—" 빈 셀 노이즈 제거 부수 효과.

## Scope (S effort, ≤0.5d)

1. `/compare` 페이지 상단에 "차이만 보기" toggle (default off).
2. on 시: 모든 vendor 컬럼에서 동일한 값 row hide. 단, 1개 vendor 만 비어 있고 나머지 채워진 경우는 표시 (의미 있는 차이).
3. localStorage 에 toggle 상태 저장 (page reload 후 유지).
4. mobile sticky-row 와 호환.

## Out of scope

- 차이 정도 grading (소소한 차이 vs 대조). 단순 diff 만.
- vendor 별 컬러 코딩.

## Acceptance

- [ ] toggle on/off 모두 정상 작동, 라이브 검증.
- [ ] 모든 row 동일 → toggle on 시 "모든 항목이 동일합니다" empty state.
- [ ] keyboard accessible (toggle button focus + ARIA).
- [ ] PR description 에 before/after gif 또는 스크린샷.

## Pre-baked policies

- 막힘 24h+ → CEO escalation. 보드 직접 ping 금지.
- compare-data 구조 변경 필요 시 CEO 에 ask, 추측 금지.
- PR 머지는 보드 권한 → 준비되면 `request_confirmation`.

## Parent

PACAA-308 (분석, done). 시퀀스 #3 → **#2** → #4 → #1.
