---
name: "[PACAA-118 위임] vendor import 코드 위치 + slug_redirects/slug_history 스키마 sign-off"
assignee: "cto"
---

PACAA-118 (P1.C Slug 정규화) 의 두 sub-task 를 CTO 에 위임.

## 1. 스키마 sign-off — `slug_redirects` + `slug_history`

현재 두 테이블 미존재. PACAA-118 의 redirect source-of-truth + 향후 모든 slug rename 의 audit trail 로 사용.

드래프트: `plans/migration_pacaa118_slug_normalize.sql` (ROLLBACK 기본, collision/dup assertion 포함).

```sql
CREATE TABLE IF NOT EXISTS slug_redirects (
    id          uuid PRIMARY KEY DEFAULT gen_random_uuid(),
    from_slug   text NOT NULL UNIQUE,
    to_slug     text NOT NULL,
    entity      text NOT NULL DEFAULT 'company',
    status_code int  NOT NULL DEFAULT 301,
    reason      text,
    created_at  timestamptz NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS slug_redirects_from_slug_idx ON slug_redirects (from_slug);

CREATE TABLE IF NOT EXISTS slug_history (
    id           uuid PRIMARY KEY DEFAULT gen_random_uuid(),
    company_id   uuid NOT NULL REFERENCES companies(id) ON DELETE CASCADE,
    old_slug     text NOT NULL,
    new_slug     text NOT NULL,
    reason       text,
    actor        text,
    created_at   timestamptz NOT NULL DEFAULT now()
);
CREATE INDEX IF NOT EXISTS slug_history_company_idx ON slug_history (company_id);
```

Path A/B 결정과 무관하게 두 테이블 자체는 필요. **승인 또
