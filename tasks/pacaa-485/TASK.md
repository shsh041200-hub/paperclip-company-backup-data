---
name: "P5 — V03 brand-* palette → V04 Stripe Purple swap (PACAA-463 Phase 5, one-way door)"
assignee: "frontend-engineer"
---

## 범위 (Phase 5, V03 brand-* palette → V04 swap)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v6-phase5.md` / **선행**: PACAA-477/479/481 모두 완료 (Phase 1-4).

### 영향 범위 (사전 grep 결과)

CEO 사전 grep — `brand-*` class 인용 매우 isolated:
- `app/globals.css` 12 토큰 정의 (palette 10 + brand-hover + brand-light).
- `app/terms/page.tsx:33` — `bg-brand-50 border-l-4 border-brand-700` (정보 박스 1).
- `app/privacy/page.tsx:42` — 동일 패턴 (정보 박스 1).
- 그 외 모든 라우트 = `brand-*` class 0 hits (Phase 1-4 에서 stripe-purple 전용 토큰으로 swap 완료).

### 수정 대상 (1 파일)

`app/globals.css` 의 12 brand-* hex 값:

```
--color-brand-50:  #FFF7ED → #F0EEFF
--color-brand-100: #FFEDD5 → #E3DFFF
--color-brand-200: #FED7AA → #C4BAFF
--color-brand-300: #FDBA74 → #A395FF
--color-brand-400: #FB923C → #806FFF
--color-brand-500: #F97316 → #533AFD  (Stripe primary anchor)
--color-brand-600: #EA580C → #4434D4  (Stripe hover anchor)
--color-brand-700: #C2410C → #3624A8
--color-brand-800: #9A3412 → #2A1C80
--color-brand-900: #7C2D12 → #1C1454
--color-brand-hover: #9A3412 → #4434D4
--color-brand-light: #FFF7ED → #F0EEFF
```

### 수정 금지

- 다른 globals.css 토큰 (info / success / warning / danger / neutral / stripe-purple V04 전용 / heading-deep-nav
