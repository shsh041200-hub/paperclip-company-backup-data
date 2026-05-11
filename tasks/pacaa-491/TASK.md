---
name: "PACAA-490 FE — 메인페이지 redesign 3-direction prototype (preview 라우트)"
assignee: "ceo"
---

## Context

부모: PACAA-490 (보드 직배정). 보드 원안:

> 메인페이지 개선안을 크롬에 띄워달라. 일관성 (살짝), 신뢰·전문성, UX 비중 더.

CEO 결정: 1안이 아니라 **3 direction prototype** 으로 design space 펼친 뒤 보드가 Chrome 에서 비교 선택. 상세 brief: `$AGENT_HOME/plans/PACAA-490-main-page-redesign.md` (CEO workspace, 같은 path 형식이 FE workspace 에도 존재 시 미러; 미존재 시 본 description 이 source of truth).

## 산출물

1. PR `feat/PACAA-490-main-page-redesign-prototypes` (base: main)
2. 3 preview 라우트:
   - `app/design-preview/main-v1/page.tsx` — Stripe-style 명료성
   - `app/design-preview/main-v2/page.tsx` — 한국 신뢰-시그널 밀도 (다나와/오늘의집)
   - `app/design-preview/main-v3/page.tsx` — Discovery-first 디렉토리 (thomasnet/houzz pro)
   - `app/design-preview/page.tsx` — 3안 비교 인덱스 (페르소나 mission 요약)
3. 모든 preview 라우트 `metadata: { robots: 'noindex,nofollow' }` 필수
4. Vercel preview deploy URL

## Lock 된 제약 (변경 금지)

- 브랜드 토큰: V04 Stripe Purple (PACAA-485 직후) — `stripe-purple-*` / `text-foreground` 등 토큰만. hex 직접 금지.
- 헤더/푸터: 기존 컴포넌트 재사용 (일관성 axis).
- 타이포·그리드: 기존 유틸 재사용 (`max-w-7xl`, `text-*`).
- production `app/page.tsx` / `app/layout.tsx` 변경 0. 이번 PR 은 preview 만.

## 3 direction 시그니처

### v1 — Stripe-style 명료성
- benchmark: stripe.com 홈
- 구조: 넓은 white space, hero 1차 CTA 1개 (구매자 검색),
