---
name: "P4a — FE-only 7 라우트 V04 토큰 적용 (PACAA-463 Phase 4)"
assignee: "frontend-engineer"
---

## 범위 (Sub-Phase 4a, FE-only routes)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v5-phase4.md` / **선행**: PACAA-477 (P3 토큰 baking 완료).

### 수정 대상 (7 라우트)
- `app/opt-out/page.tsx`
- `app/opt-out/thanks/page.tsx`
- `app/services/[slug]/page.tsx`
- `app/use-cases/[slug]/page.tsx`
- `app/keywords/page.tsx`
- `app/keywords/[slug]/page.tsx`
- `app/compare/page.tsx`
- `app/compare/[slug]/page.tsx`

### 수정 금지
- `app/guides/*`, `app/blog/*` — Sub-Phase 4b (CMO 조율 후 별도 child).
- `app/terms`, `app/privacy`, `app/sitemaps/*` — 본 Phase 범위 외.
- `app/page.tsx`, `app/companies/[slug]`, `app/categories/*`, `app/products/[slug]` — Phase 1-3 산출물 회귀 0 유지.
- `app/globals.css` — Phase 3 토큰 추가 완료, 추가 토큰 필요 시 본 issue 코멘트로 escalate.

### 참조 자료
`packlinx-design-system` 스킬 + Phase 3 토큰 (`text-stripe-purple`, `text-heading-deep-navy`, `text-body-secondary`, `border-border-v04`, `shadow-elevated-v04`, `heading-display` utility 등).

## Acceptance Criteria

1. **토큰 클래스 적용** — 7 라우트 모두 V03 hex 인용 → V04 토큰 클래스 swap. broader grep `533afd|061b31|e5edf5|rgba(50,50,93` post-PR = 라우트별 ≤2 (코멘트만 OK).
2. **회귀 0** — Phase 1-3 산출 5 라우트 (vendor/main/categories x2/products) 변경 0줄. PR diff stat 명시.
3. **V03 palette
