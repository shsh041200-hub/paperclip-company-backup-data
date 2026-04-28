---
name: "[PACAA-30] category_denominators 스키마 CTO sign-off"
assignee: "backend-engineer"
---

## 배경

[PACAA-30](/PACAA/issues/PACAA-30) P1.1 분모 산출 시스템 구현을 위한 스키마 설계입니다.
SG-3 측정 인프라와 공유되는 테이블이므로 CTO 사인오프 필요 ([PACAA-25](/PACAA/issues/PACAA-25) plan v3 §3 cross-cut).

## 검토 요청 스키마

### 테이블 1: category_denominators

```sql
CREATE TABLE category_denominators (
  id                    uuid PRIMARY KEY DEFAULT gen_random_uuid(),
  category_key          text NOT NULL,         -- e.g., 'corrugated_box'
  category_name_ko      text NOT NULL,         -- e.g., '골판지·종이박스'
  ksic_codes            text[] NOT NULL,        -- e.g., ARRAY['1721','1722']
  ksic_description      text,
  denominator_estimate  integer NOT NULL CHECK (denominator_estimate > 0),
  estimate_low          integer CHECK (estimate_low > 0),
  estimate_high         integer CHECK (estimate_high > estimate_low),
  confidence_level      text NOT NULL DEFAULT 'medium'
                          CHECK (confidence_level IN ('high','medium','low')),
  source_primary        text NOT NULL,
  source_url            text,
  source_reference_year integer NOT NULL,
  source_attribution    jsonb NOT NULL DEFAULT '{}',
  method_version        text NOT NULL,         -- e.g., 'v1.0-bootstrap', 'v2.0-kosis-api'
  method_notes          text
