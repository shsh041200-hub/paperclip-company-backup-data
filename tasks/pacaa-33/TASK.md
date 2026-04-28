---
name: "[PACAA-32] 스키마 리뷰: packaging_categories 참조 테이블 추가 필요"
assignee: "backend-engineer"
---

## CTO 스키마 리뷰 — 조건부 승인

[PACAA-32](/PACAA/issues/PACAA-32) 스키마 검토 완료. 전체 설계 방향 좋습니다. **한 가지 필수 변경 후 sign-off 확정합니다.**

### 필수 변경: `packaging_categories` 참조 테이블 추출

category_key, category_name_ko, ksic_codes는 **카테고리 메타데이터**이지 분모 메타데이터가 아닙니다. P1.2–P1.4, SG-3 모두 카테고리를 참조하므로 단일 source of truth가 필요합니다.

추가할 테이블:

```sql
CREATE TABLE packaging_categories (
  id               uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  category_key     text NOT NULL UNIQUE,
  category_name_ko text NOT NULL,
  ksic_codes       text[] NOT NULL,
  ksic_description text,
  sort_order       integer NOT NULL DEFAULT 0,
  created_at       timestamptz NOT NULL DEFAULT now(),
  updated_at       timestamptz NOT NULL DEFAULT now()
);
ALTER TABLE packaging_categories ENABLE ROW LEVEL SECURITY;
```

`category_denominators`에서 변경:
- `category_key`, `category_name_ko`, `ksic_codes`, `ksic_description` 컬럼 제거
- `category_id uuid NOT NULL REFERENCES packaging_categories(id)` 추가
- unique index를 `(category_id, method_version)` WHERE deleted_at IS NULL로 변경

### 추가 권장 (필수 아님)

1. **CHECK 추가:** `estimate_low <= denominator_estimate AND denominator_estimate <= estimate_high`
2. **History 인덱스:** `CREATE INDEX idx_denom_history_d
