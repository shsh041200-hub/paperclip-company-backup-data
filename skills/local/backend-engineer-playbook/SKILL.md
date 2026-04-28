---
name: "backend-engineer-playbook"
description: "Backend engineer specialty playbook — runbook scoped to the Packlinx Supabase + Postgres + Edge Functions stack covering schema discipline, RLS, migration safety, and the data-integrity rules that protect vendor records."
slug: "backend-engineer-playbook"
metadata:
  paperclip:
    slug: "backend-engineer-playbook"
    skillKey: "local/7e02d38144/backend-engineer-playbook"
  paperclipSkillKey: "local/7e02d38144/backend-engineer-playbook"
  skillKey: "local/7e02d38144/backend-engineer-playbook"
key: "local/7e02d38144/backend-engineer-playbook"
---

# Backend Engineer Playbook

Specialty bundle for the Packlinx Backend Engineer role. Scoped to the
actual stack: Supabase (Postgres 15+), pg_cron, Edge Functions (Deno),
TypeScript, Next.js 16 server-side handlers.

Common skills handle voice, decision protocol, and company context. Do not
duplicate that content here.

## When to invoke this skill

- Designing or modifying a database schema
- Writing or reviewing a migration
- Touching anything that mutates vendor data
- Designing or modifying RLS policies
- Writing an Edge Function or background job
- Debugging a data-integrity issue

## First principle

**Vendor data is the moat. A wrong insert that gets rendered as truth
costs more than a slow page.** Every backend decision passes through that
filter first.

## Schema discipline

### Naming

- `snake_case` everywhere — tables, columns, functions.
- Tables: plural (`vendors`, `categories`, `vendor_certifications`).
- Junction tables: alphabetical pairs (`vendors_categories`, not
  `categories_vendors`).
- Boolean columns named for the *true* state (`is_verified`, not
  `not_verified`).
- Timestamps: `created_at`, `updated_at`, `deleted_at` (soft delete).

### Column rules

- Every table has `id uuid primary key default gen_random_uuid()`.
- Every table has `created_at timestamptz not null default now()`.
- Every table has `updated_at timestamptz not null default now()` with
  a trigger to update on UPDATE.
- Soft delete via `deleted_at timestamptz` is preferred to hard DELETE
  for vendor-touching tables.
- Foreign keys are explicit — `references vendors(id) on delete restrict`
  unless cascade is genuinely intended (rarely).
- `not null` is the default; nullable is the exception with a reason.

### Indexes

- Index every foreign key.
- Index every column used in `WHERE` or `ORDER BY` for paths in the hot
  read set.
- Composite indexes match query patterns (column order matters).
- Verify with `EXPLAIN ANALYZE` before assuming an index is used.
- Drop indexes that aren't being read (`pg_stat_user_indexes` zero scans
  for 30+ days → candidate for removal).

### Korean text columns

- `text` (not `varchar(N)`) unless there's a real upstream constraint.
- Collation: `und-x-icu` for Korean-comparison-aware sort. Default
  collation breaks 한글 ordering.
- Trim and NFC-normalize on insert via trigger or application layer.
  Never store mixed forms.

## Migrations

### The migration safety rule

Every migration is reversible OR explicitly marked one-way with a
documented exit cost in the PR description. No exceptions for vendor-
touching tables.

### Migration shape

- Numbered, idempotent where possible.
- Up + Down. Down must restore the schema (data loss is acceptable on
  Down only with explicit consent in the PR).
- Tested locally against a snapshot of production-shape data.
- Reviewed by the CTO before any vendor-touching migration runs.

### Risky migrations — the slow path

For tables with > 100k rows or vendor-touching tables:

- Add column NULLABLE first, even if it'll eventually be NOT NULL.
- Backfill in batches via pg_cron or a scripted loop. Never
  single-statement `UPDATE table SET col = ...` on a large table —
  it locks the table.
- Once backfilled, add the NOT NULL constraint in a separate migration.
- Index creation on large tables: `CREATE INDEX CONCURRENTLY` so writes
  aren't blocked.
- Schema rename / type change: dual-write window — keep old + new,
  cut over reads, drop old. Each step is a separate deploy.

### Anti-patterns

- `DROP COLUMN` without a deprecation window.
- `DROP TABLE` without a 30-day soft-delete period.
- Single-statement backfill on a > 1M row table.
- "Just clean up the data manually in production" — every manual
  edit is a future audit failure.

## Row Level Security (RLS)

### Default

RLS is **on** for every public schema table. Default deny. Explicit
allow.

### Policy patterns

- **Anonymous (read-only public surfaces):** Single SELECT policy with
  the minimum visible columns enforced via a view, not by trusting the
  client.
- **Authenticated user (vendor portal):** Policy checks
  `auth.uid() = owner_user_id` or join through a membership table.
- **Service role:** Bypasses RLS by design. Service-role keys must
  never reach the browser. Use server-only routes.
- **Admin (board / CEO):** Separate role + policy. Don't reuse
  `service_role` for human admin actions; you lose audit clarity.

### RLS pitfalls

- Forgetting RLS on a new table — it's permissive by default if you
  forget to ENABLE. Always `ALTER TABLE x ENABLE ROW LEVEL SECURITY`
  in the same migration that creates the table.
- Policies that reference functions that themselves bypass RLS
  internally — security holes hidden one layer down.
- Using `current_user` instead of `auth.uid()` — `current_user` is the
  Postgres role, not the application user.

## Vendor data path

- Every mutation logs to an audit table:
  `vendor_audit (id, vendor_id, action, actor_id, actor_type,
  field_diff jsonb, evidence_url, created_at)`.
- Insert / update via stored procedure when the validation logic is
  non-trivial — keeps the rules in one place.
- "Replace" is never silent. Either merge with a documented strategy
  or reject with a clear error.
- Bulk imports: staging table → validation → atomic copy into vendors.
  No direct INSERT INTO vendors from an external file.

## Edge Functions

- TypeScript only. No JavaScript without types in production.
- One function per concern. Don't pile unrelated routes into one
  function for "deployment ease."
- Timeouts: explicit per call. Default to 10s; document anything
  longer.
- Idempotency: every mutation handler accepts an `Idempotency-Key`
  header. Critical for retry-safe vendor operations.
- Secrets: via Supabase secrets, never in code, never in env files
  committed to the repo.
- Logging: structured (JSON), with `vendor_id`, `request_id`,
  `actor_id` on every mutation log line.

## Background jobs (pg_cron)

- All scheduled jobs live in a single migration file so the catalog
  is greppable.
- Every job has a max execution time. Long-running jobs run as a
  loop of small batches, not a single statement.
- Jobs that touch vendor data write an audit row per run.
- Failure handling: jobs that fail twice in a row alert via a webhook;
  don't silently retry forever.

## Performance

- N+1 detection: use Supabase's logging dashboard or pg_stat_statements
  weekly. The most common backend perf bug is the front-end calling a
  list endpoint that issues per-row queries.
- Pagination: cursor-based (id + created_at), not offset. Offset is
  wrong-feeling at scale and breaks under concurrent inserts.
- Connection pooling: PgBouncer through Supabase, transaction mode for
  most workloads. Session mode only when you need session-level state
  (rare).

## Testing

- Unit tests for non-trivial pure functions (validation, parsing).
- Integration tests for handlers that hit Postgres — against a real
  test database, not a mock.
- Migration tests: each migration runs against a snapshot, then Down
  runs, then Up runs — no drift.
- Seed data is realistic shape, not "foo / bar / baz" — Korean
  characters, edge-case lengths, real-shape categories.

## PR checklist

- [ ] Migration is reversible or explicitly marked one-way.
- [ ] RLS policies exist on every new table; default deny.
- [ ] Foreign keys + indexes match query patterns.
- [ ] Korean text columns: `text`, NFC, collation set.
- [ ] Audit row written for every vendor-touching mutation.
- [ ] No service-role key path reachable from the browser.
- [ ] Tests cover the new path (against real Postgres).
- [ ] EXPLAIN ANALYZE checked for new hot queries.

## Refusals

- Refuse to ship a migration that mutates vendor data without a
  rollback path.
- Refuse to disable RLS on a public-schema table.
- Refuse to put service-role credentials in any code that runs
  client-side or in an unauthenticated public function.
- Refuse to skip the audit log for "small" vendor changes — small is
  how data drift starts.
- Refuse to manually edit production data outside a migration; if it
  must happen, it's a migration with a PR.

## Self-check

- [ ] If this change broke vendor data tomorrow, could I reverse it
      with the audit trail and the migration?
- [ ] Are RLS policies covering every realistic actor (anon, user,
      vendor-owner, admin, service)?
- [ ] Did I run `EXPLAIN ANALYZE` on the new query paths?
- [ ] Is the migration safe on a table with 10× current row count?
