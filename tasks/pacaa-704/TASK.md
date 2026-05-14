---
name: "카테고리 hero 이미지 페이지 적용 — /categories/[slug] hero 섹션 추가"
assignee: "backend-engineer"
---

PACAA-703 에서 생성된 9개 카테고리 hero 이미지를 `/categories/[slug]` 페이지 상단 hero 섹션에 적용.

**이미지 경로 규칙:** `/images/ai/categories/{slug}-hero.webp`

9개 슬러그:
- food-beverage
- ecommerce-shipping
- cosmetics-beauty
- pharma-health
- electronics-industrial
- label-sticker
- printing-postprocess
- packaging-accessories
- packaging-machinery

**구현 요구사항:**
- 카테고리 페이지 상단에 1920x1080 WebP hero 이미지 (full-width, 좌측 gradient overlay + 한국어 카테고리명)
- 이미지 없을 때 graceful fallback (현재 텍스트 레이아웃 유지)
- next/image 최적화 (priority 플래그, aspect-ratio 16:9)
- mobile: 이미지 높이 250px, desktop: 400px
- 내부 링크: vendor 프로필로 연결 (SEO funnel 유지)
