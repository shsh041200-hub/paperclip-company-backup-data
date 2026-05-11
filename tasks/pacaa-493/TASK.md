---
name: "PACAA-490 FE r2-v3 polish — 가이드 영역 ↔ 카테고리/vendor 영역 시각 분리 강화"
assignee: "ceo"
---

## Context

부모: PACAA-490. 보드 답변 (PACAA-490 코멘트 5855682b, 2026-05-11 00:50 KST):

> r2-v3가 맘에 들어 근데 패키징 가이드 칸은 좀더 카테고리 영역과 좀 분리되었으면 좋겠어 이것만 해결해서 보여줘봐 크롬으로

v3 (Sidebar Directory) 픽 — 보드 polish 1건 후 production swap (Phase 2) 별 child 발의.

## 작업 범위 (preview 라우트 polish only)

대상: `app/design-preview/main-r2-v3/page.tsx` 만. Production `app/page.tsx` 변경 0 (Phase 2 별 child 에서).

### 1. 가이드 섹션 시각 분리 강화 (필수)

현재 구조 (라이브 확인):
- main pane: slim hero → 식품·음료 vendor 6개 그리드 ("카테고리 영역") → 패키징 가이드 3개 ("가이드 영역")

보드 의도: 가이드 영역이 카테고리/vendor 영역과 시각적으로 좀 더 분리되어야 함.

해결 axis (FE 결정 — 1개 또는 조합):

- (a) **수직 spacing 증가** — 가이드 섹션 위 mt 강화 (mt-12 → mt-20 또는 24)
- (b) **horizontal divider** — 가이드 섹션 위 border-t border-stripe-purple-100 또는 muted (얇게, 1px)
- (c) **background wash** — 가이드 섹션 wrap 에 bg-stripe-purple-50/30 또는 bg-card 으로 surface 차이
- (d) **eyebrow 강화** — 가이드 섹션 heading 위 eyebrow 라벨 ("전문성" 또는 "학습") + heading 의 typographic 위계 강화
- (e) **컨테이너 분리** — main pane 내에서 가이드 섹션만 다른 max-w 또는 padding 차이로 "다른 영역" 신호

권장 = b + c + d 조합. 단, (c) 의 wash 는 monochrome lock 위반 의심 — stripe-purple-50 (color-mix 가 아닌 pure neutral-tinted) 만 OK, hex 사용 금지. 의심 시 b + d 만.

### 2. v3 metadata 결함 동시 fix (선택, 권장)

현재 v3 가 `'use
