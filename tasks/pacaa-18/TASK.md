---
name: "카테고리 개선: 분류기 단일화 + CompanyTag enum 폐기"
assignee: "cto"
project: "packlinx-website"
---

## 목표

분류 신호를 단일화. CompanyTag enum 폐기 + classifier.ts 룰 통합.

## 범위

### 변경 사항

**CompanyTag 6종 분석:**

| Tag | 현재 의미 | 처리 |
|---|---|---|
| `food_grade` | IndustryCategory.food-beverage 와 사실상 1:1 | 제거 (중복) |
| `industrial` | IndustryCategory.electronics-industrial 와 1:1 | 제거 |
| `cosmetic` | IndustryCategory.cosmetics-beauty 와 1:1 | 제거 |
| `pharma` | IndustryCategory.pharma-health 와 1:1 | 제거 |
| `design_service` | `/services/printing-design` 으로 흡수 | 제거 |
| `ecommerce` | IndustryCategory.ecommerce-shipping 와 1:1 | 제거 |

→ **CompanyTag enum 자체 삭제.**

### 구현 가이드

- `src/types/index.ts`에서 `CompanyTag` enum + `TAG_LABELS` 제거.
- `src/lib/crawler/classifier.ts`:
  - `TAG_RULES` 상수 + `detectTags()` 함수 제거.
  - `ClassificationResult.tags` 필드 제거.
  - `WEIGHTED_INDUSTRY_RULES`만 유지 (이게 단일 산업 분류 신호가 됨).
- `src/lib/crawler/ai-classifier.ts`도 tags 출력하면 동일하게 제거.
- `src/lib/crawler/pipeline.ts`에서 tags 컬럼 저장 부분 제거.
- Supabase 마이그레이션:
  - `companies.tags` 컬럼 삭제 (또는 deprecated 처리 후 다음 단계 제거).
  - 기존 tags 값 기반으로 누락된 IndustryCategory 보정 1회 SQL 실행 (예: tag=`pharma`인데 industry_categories에 `pharma-health` 없으면 추가).
- vendor 일괄 재분류 불필요 — 기존 산업 분류는 보존, tags만 폐기.

### 산출물

- CompanyTag enum 제거.
- classifier.ts 룰
