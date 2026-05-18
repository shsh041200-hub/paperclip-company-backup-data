---
name: "[FE][SEO] /guides/[slug] dynamic guides 17개 Article JSON-LD 누락 — FAQPage만 있음"
---

GuideSlotV1Page (app/guides/[slug]/page.tsx)는 FAQPage JSON-LD만 출력. 정적 가이드(label-printing-guide, plastic-container-guide, flexible-packaging-guide)는 Article JSON-LD(datePublished, dateModified, author, publisher, image)를 포함하지만, 동적 슬러그 17개는 Article 스키마가 없음. Naver/Google Rich Result에서 Article 신호 누락.

## 수정 범위
- GuideSlotV1Page에 Article JSON-LD 추가 (headline, description, url, datePublished, dateModified, author, publisher, image)
- slug prop을 GuideSlotV1Page에 전달
- 17개 동적 가이드 슬러그 모두 적용
