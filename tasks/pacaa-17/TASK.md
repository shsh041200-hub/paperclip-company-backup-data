---
name: "카테고리 개선: IndustryCategory 정리 + 슬러그 통일 (kebab-case)"
assignee: "cto"
project: "packlinx-website"
---

## 목표

L1 산업 카테고리(IndustryCategory) 정리 + 슬러그 네이밍 통일.

## 범위

### 변경 사항

**유지 (5개, kebab-case 통일):**
- `food-beverage` — `fresh_produce_packaging` 흡수 (모든 vendor를 food-beverage로 재라벨)
- `cosmetics-beauty`
- `pharma-health`
- `electronics-industrial`
- `ecommerce-shipping`

**제거:**
- `eco-special` — 패싯 필터 "친환경 인증"으로 강등 (PACAA-15.4에서 패싯화). 이 티켓에서는 IndustryCategory에서만 제거하고 vendor의 인증 필드는 보존.
- `fresh_produce_packaging` — `food-beverage`에 흡수. boolean 패싯 "신선·콜드체인"은 PACAA-15.4에서 추가.
- `print_design_services` — 본 티켓 시점에는 PACAA-15.1로 이미 `/services/printing-design` 신설됨. IndustryCategory enum에서 제거하고 vendor를 services 라우트가 보고 있는 새 분류 키로 마이그레이션.

### 구현 가이드

- `src/types/index.ts`의 `IndustryCategory` enum 정리 (5종으로 축소).
- `INDUSTRY_CATEGORY_LABELS`, `_DESCRIPTIONS`, `_ICONS` 동기화.
- Supabase 마이그레이션 신규 작성:
  - `companies` 테이블의 산업 카테고리 컬럼(`industry_categories[]` 또는 단일 컬럼) 일괄 재라벨.
  - `fresh_produce_packaging` → `food-beverage` (단순 치환).
  - `eco-special` 보유 vendor는 `is_eco = true` boolean 컬럼으로 마킹 (없으면 추가).
  - `print_design_services` 보유 vendor는 별도 `is_print_design_service = true` boolean으로 마킹 + services 라우트 쿼리에 사용.
- `categoryGuide.ts`에서 제거된 3개 슬러그 항목 삭제.
- `/categories/[slug]` 라우트의 `[slug]` 매칭 가능 값을 5
