---
name: "[FE][SEO] Naver keywords 메타 + hreflang ko-KR 일괄 추가 (7개 파일)"
assignee: "frontend-engineer"
---

## 배경

Naver는 `<meta name="keywords">` 태그를 여전히 부분적으로 고려함. 현재 /categories/[slug] generateMetadata에 keywords 필드 없음.

`CATEGORY_KEYWORDS` 상수가 각 카테고리별 타겟 키워드를 이미 정의하고 있음 (예: ecommerce-shipping → [골판지박스 제작, 택배박스 제작, 소량 박스 제작, 박스 견적]). 이 데이터를 metadata keywords로 노출.

## 작업 범위

- `app/categories/[slug]/page.tsx`: generateMetadata에 `keywords: CATEGORY_KEYWORDS[categoryKey].map(k => k.label)` 추가
- 단일 파일 변경

## Done 기준
- PR 생성 + in_review
