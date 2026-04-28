---
name: "카테고리 개선: /products 10개 + /services/printing-design 라우트 신설"
assignee: "cto"
project: "packlinx-website"
---

## 목표

신규 3축 구조의 첫 번째 축 + 세 번째 축 라우트·페이지 신설.

## 범위

### 신설 라우트

**`/products/[slug]` — 10개:**

| 슬러그 | 라벨 | PackagingForm 매핑 |
|---|---|---|
| `box` | 박스·케이스 | `box_case` |
| `pouch` | 파우치·백 | `pouch_bag` |
| `container` | 병·용기 | `bottle_container` |
| `tube` | 튜브 | `tube` |
| `can` | 캔·틴 | `can_tin` |
| `shopping-bag` | 쇼핑백·캐리어백 | `shopping_bag` |
| `cushioning` | 완충재·보호재 | `cushioning` |
| `film` | 스트레치·필름 | `stretch_film` |
| `label` | 라벨·스티커 | `label_sticker` |
| `tape` | 테이프·밀봉재 | `tape_sealing` |

**`/services/[slug]` — 1개:**

| 슬러그 | 라벨 | 출처 |
|---|---|---|
| `printing-design` | 인쇄·디자인 서비스 | 현 `IndustryCategory.print_design_services` 이전 |

### 구현 가이드

- `src/app/products/[slug]/page.tsx` 및 `src/app/services/[slug]/page.tsx` 신설.
- 기존 `src/app/categories/[slug]/page.tsx` 패턴 재사용 — 카테고리 히어로 + 필터 바 + 업체 그리드 + 페이지네이션.
- vendor 쿼리: products는 `companies.packaging_form` 컬럼 매칭. services는 `IndustryCategory = 'print_design_services'` 인 vendor + PrintDesignSubtype 필터.
- `src/data/categoryGuide.ts` 패턴 따라 `productGuide.ts` / `serviceGuide.ts` 신규 작성 — 각 슬러그별 description / buyerPoints / subTypes / seoKeywords.
- 기존 `/categories/[slug]` 라우트는 PACAA-15.2까지 함께 유지(병행 운영). 본 티켓에서는 제거 금지.

### 산출물
