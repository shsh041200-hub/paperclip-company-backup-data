---
name: "상단바 통일 — SiteHeader 추출 + production 라우트 전수 교체 (PACAA-632)"
assignee: "ceo"
---

부모: PACAA-632 — 보드 지시 "상단바를 페이지 홈(www.packlinx.com /) 기준으로 전부 통일".

## 기준 헤더 (홈 / app/page.tsx:377-394)


## 작업
1. components/SiteHeader.tsx 신규 — 위 마크업 그대로.
2. 홈 page.tsx inline 헤더를 <SiteHeader/> 호출로 교체.
3. 아래 production 라우트 자체 헤더 전수 교체:
   - /categories, /categories/[slug]
   - /companies/[slug]
   - /compare, /compare/[slug]
   - /match
   - /guides (app/guides/layout.tsx)
   - /faq (app/faq/FaqClient.tsx)
   - /keywords, /keywords/[slug]
   - /products/[slug], /services/[slug], /use-cases/[slug]
   - /opt-out, /opt-out/thanks
   - /privacy, /terms
   - /blog/* (2 posts)
4. Skip /design-preview/* (샌드박스).

## Acceptance
- grep -rn "<header" app/ | grep -v design-preview = SiteHeader.tsx 만 매칭, production 0건.
- npm run build 통과.
- npm run dev 띄워 /, /categories, /companies/<slug>, /match, /guides, /faq, /keywords 스폿체크.
- nav 4종 (로고→/, 전체업체→/, 카테고리→/categories, 가이드→/guides) 200.

## 가드
- 푸터·본문 변경 금지 (헤더만).
- Tailwind 토큰 의미 변경 금지.
- PR title 에 PACAA-632 포함.

완료 시 PR 머지 → PACAA-632 final 코멘트.
