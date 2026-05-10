---
name: "P3 — V04 토큰 hard-bake + 5 라우트 migration (PACAA-463 Phase 3)"
assignee: "frontend-engineer"
---

## 범위 (P3 token hard-bake, additive)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v4-phase3.md` / **선행**: PACAA-464 (P1), PACAA-473 (P2).

### 파일

1. `app/globals.css` — `@theme` 블록 끝에 V04 토큰 추가 (additive). 기존 V03 `--color-brand-*` palette **미변경**. utility class `.heading-display` 추가.
2. 5 V04 라우트 — inline hex → 토큰 클래스 swap:
   - `app/companies/[slug]/page.tsx`
   - `app/page.tsx`
   - `app/categories/page.tsx`
   - `app/categories/[slug]/page.tsx`
   - `app/products/[slug]/page.tsx`

### 추가할 토큰 (semantic)

```css
--color-stripe-purple: #533afd;
--color-stripe-purple-hover: #4434d4;
--color-stripe-purple-soft: rgba(83, 58, 253, 0.05);
--color-stripe-purple-tint: rgba(83, 58, 253, 0.08);
--color-stripe-purple-ring: rgba(83, 58, 253, 0.12);
--color-heading-deep-navy: #061b31;
--color-body-secondary: #64748d;
--color-border-v04: #e5edf5;
--shadow-elevated-v04: rgba(50,50,93,0.25) 0px 30px 45px -30px, rgba(0,0,0,0.10) 0px 18px 36px -18px;
--font-heading-display: 'sohne-var', 'SF Pro Display', -apple-system, sans-serif;
```

`.heading-display` utility (font-feature-settings 토큰 미지원 우회):
```css
.heading-display {
  font-family: var(--font-heading-display);
  font-weight: 300;
