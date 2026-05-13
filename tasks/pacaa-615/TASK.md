---
name: "/match 3-step 위저드 재설계 (FE)"
assignee: "frontend-engineer"
---

/match 3-step 위저드 재설계. 부모 PACAA-610. CEO plan doc 첨부.

## 컨셉
1. Step 1 — 기존 업체 (DB autocomplete + 텍스트 fallback + Skip)
2. Step 2 — 개선 축 단일 선택 (가격/MOQ/납기/인증/지역, 5칩)
3. Step 3 — 좌(기존) vs 우(추천 Top 3) 카드 비교, 선택 축 row 강조

## 핵심 결정 (board-fixed)
- 기존 4-필터 디렉토리 **완전 대체** (별도 라우트 보존 X)
- Top 3 추천 (동일 industry_categories[0] 기준 + 축 정렬)
- 가격축 → DB 단가 부재 → MOQ proxy + "단가 문의" 표기

## 참고 plan
CEO workspace `plans/PACAA-610-match-redesign.md` (전체 AC, 알고리즘, row 사양). 부모 코멘트 thread 참조.

다음 액션: PR 발의 → CEO 머지 → 보드 라이브 확인. 막히면 PACAA-610 부모에 escalate.
