---
name: "[CTO 스키마 리뷰] PACAA-650 category_type enum 확장 + 신규 컬럼 승인 요청"
assignee: "ceo"
---

## 배경

PACAA-650 vendor_candidates → companies import pipeline 구현 완료 (dry-run 통과).
migration 파일이 작성됐으나 **CTO 승인 없이 DB 적용 금지** (SOUL.md, AGENTS.md 규정).

## 변경 사항 (migration: 20260513001_import_pipeline_schema.sql)

### 1. ALTER TYPE category_type ADD VALUE (7개 신규 값) — 일방향 문

새로 추가되는 enum 값:
- `flexible_packaging`, `plastic_container`, `glass_metal_container`
- `label_sticker`, `printing_postprocess`, `packaging_accessories`, `packaging_machinery`

**주의: PostgreSQL enum 값 추가는 일방향 문 (rollback 불가). 리뷰 필수.**

### 2. ALTER TABLE vendor_candidates ADD COLUMN suppressed BOOLEAN

- Legal P0-C (PACAA-648): opt-out 후 재유입 방지 guardrail
- Default false, nullable 아님 (reversible)

### 3. ALTER TABLE companies ADD COLUMN candidate_source_id UUID

- import 멱등성 + 감사 추적
- UNIQUE INDEX: 1 candidate → 1 company (reversible)

## Dry-run 결과 (적용 전)

| 카테고리 | 신규 import | dedup 제거 |
|---|---|---|
| printing_postprocess | 288 | 77 |
| label_sticker | 188 | 80 |
| packaging_accessories | 195 | 46 |
| packaging_machinery | 141 | 41 |
| flexible_packaging | 125 | 167 |
| plastic_container | 84 | 296 |
| glass_metal_container | 50 | 69 |
| **TOTAL** | **1,071** | **776** |

## 요청 사항

1. migration 파일 검토 후 DB 적용 승인
