---
name: "[BE] Supabase unused-table audit + safe cleanup"
assignee: "backend-engineer"
---

## 목적

Supabase production DB 의 안 쓰는 데이터 테이블 식별 후 안전 삭제.

보드(`5b8744a6`)가 PACAA-935 closeout 직후 요청. PACAA-935 (website enrichment) 와 별개 스코프이므로 follow-up 이슈로 분리.

## 작업 단계 (게이트 분리)

### Phase 1 — Read-only Audit (BE 단독, mutation 0)
1. `information_schema.tables` 로 public schema 전체 테이블 목록 (`size_bytes`, `row_count`, `last_modified_at` 포함)
2. 각 테이블별로 다음 grep:
   - `pkging-platform/` repo 전체 grep (`*.ts`, `*.tsx`, `*.sql`, `*.mjs`, `*.py`)
   - `site/scripts/` enrichment 스크립트 grep
   - Supabase Studio FK references / RLS policies / functions
3. 결과 분류표 작성:
   - **Keep** (active production reads/writes)
   - **Migration legacy** (one-time import 후 미사용)
   - **Enrichment intermediate** (v3/v4/v5 의 source/staging, 이미 companies 로 머지된 데이터)
   - **Unknown** (참조는 없지만 외부 워크플로우 가능성)
4. CEO 에 분류표 코멘트 → CEO 가 보드에 per-table confirmation

### Phase 2 — Per-table Board Confirmation (CEO)
- Keep: 그대로 유지
- Migration legacy / Enrichment intermediate: 보드에 일괄 confirmation (테이블별 사이즈/내용 요약 포함)
- Unknown: 보드 개별 판단 요청

### Phase 3 — Safe DROP (BE)
1. 승인된 테이블 각각:
   - `pg_dump` 로 schema+data 백업 → `runs/supabase_drop_backup_<table>_<date>.sql.gz`
   - `DROP TABLE IF EXISTS <name> CASCADE;` 마이그레이션 PR
   - GitHub
