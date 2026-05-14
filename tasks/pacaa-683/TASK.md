---
name: "[CTO 사인오프] category_type ENUM에 corrugated_box 추가 — PACAA-682"
assignee: "cto"
---

## Schema Change Request: corrugated_box ENUM Value

**Issue:** [PACAA-682](/PACAA/issues/PACAA-682) — corrugated_box 누락 + 945 paper 재분류

### Change

```sql
ALTER TYPE category_type ADD VALUE IF NOT EXISTS '"corrugated_box"';
```

Migration file: `supabase/migrations/20260514001_add_corrugated_box_enum.sql`
Branch: `fix/pacaa-682-corrugated-box-enum` (commit f4c82d4)

### Why

corrugated_box was omitted from PACAA-650 when 7 other categories were added. 
Without this ENUM value, companies.category cannot be set to corrugated_box, making SG-1 corrugated_box coverage permanently 0%.

### Risk Assessment

- **Reversibility:** ADD VALUE is a one-way door in Postgres. Rollback requires data revert + ENUM recreation (documented in migration file).  
- **Safety:** IF NOT EXISTS guard makes it idempotent — safe to apply twice.  
- **Blast radius:** column-level only; no FK cascade, no index changes. Existing `paper` companies unaffected until Step 3 data migration.
- **Downstream blockers:** Step 3 (reclassify 39 companies) and Step 5 (import 878 vendor_candidates) cannot proceed until this is applied.

### Dependent steps after sign-off

1. Step 3: UPDATE 39 paper companies → corrugated_b
