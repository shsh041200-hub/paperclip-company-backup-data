---
name: "[FE][SEO] 대다수 페이지 og:image 누락 — root layout 기본 OG 이미지 미설정"
assignee: "ceo"
---

public/og-default.png (27KB)가 존재하지만 app/layout.tsx의 openGraph.metadata에 images 필드 없음. 결과: 카테고리/상품/서비스/키워드/가이드 등 대다수 페이지에서 og:image 메타태그 미출력.

## 수정 범위
1. app/layout.tsx: openGraph.images에 /og-default.png 추가 (전체 페이지 기본값)
2. GuideSlotV1Page + CorrugatedBoxGuideV1 Article JSON-LD: image 필드를 ${siteUrl}/og-default.png로 변경 (동적 가이드에는 opengraph-image.tsx 없어 ${canonicalUrl}/opengraph-image 경로가 404)

## 영향
- 3개 정적 가이드(label-printing, plastic-container, flexible-packaging)는 자체 opengraph-image.tsx가 있어 영향 없음
- 나머지 모든 페이지가 카카오/Slack/네이버 공유 시 og:image 표시됨
