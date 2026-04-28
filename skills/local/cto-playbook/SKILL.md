---
name: "cto-playbook"
description: "CTO specialty playbook — architecture decision (ADR) template for one-way-door technical choices and a code-review checklist scoped to the Packlinx Next.js 16 + Supabase + Postgres stack. Read before authoring an ADR or reviewing a non-trivial PR."
slug: "cto-playbook"
metadata:
  paperclip:
    slug: "cto-playbook"
    skillKey: "local/449478da2a/cto-playbook"
  paperclipSkillKey: "local/449478da2a/cto-playbook"
  skillKey: "local/449478da2a/cto-playbook"
key: "local/449478da2a/cto-playbook"
---

# CTO Playbook

Specialty bundle for the Packlinx CTO role. Covers two recurring artifacts: architecture decisions and stack-scoped code review.

Common skills (`packlinx-context`, `packlinx-comms`, `packlinx-decision-log`,
`benchmark-methodology`, `encoding-discipline`) handle voice, decision protocol,
and company context. Do not duplicate that content here.

## When to invoke this skill

- Drafting or reviewing an Architecture Decision Record (ADR)
- Reviewing a PR that touches schema, auth, vendor data, or production config
- Choosing a third-party service, library, or hosting model
- Writing a technical proposal that the CEO or board will read

Skip for: trivial bugfixes, cosmetic UI tweaks, dependency bumps with no API
change.

## Part 1 — Architecture Decision Record (ADR)

### When to write an ADR

Write one when the decision is **hard to reverse** — schema, vendor lock-in,
auth model, data ownership, billing model. Skip for two-way-door choices like
file structure or naming. The test: "if we change our minds in 6 months, does
this require a migration, a contract exit, or a rewrite?" If yes, ADR.

### Filename convention

`runs/<YYYY-MM-DD>-adr-<short-slug>.md` in the CTO workspace, plus a copy as
the issue's `plan` document on the originating ticket.

### ADR template

```md
# ADR — <Decision in one line>

**Date:** <YYYY-MM-DD>
**Status:** proposed | accepted | superseded by <link>
**Issue:** <PACAA-NN link>
**Reversibility:** one-way | two-way (cost to reverse: <hours/days/$>)

## Context

What is the problem? What constraints are fixed? What changed that forces a
decision now? Two paragraphs max. State the smallest version that still
captures why this is a real decision and not a default.

## Options considered

At least two real options. A single option is a default, not a decision.

### Option A — <name>

- What it is in one sentence.
- Pros (concrete, not generic).
- Cons (concrete, not generic).
- Cost: build $/time, recurring $/month, exit cost.

### Option B — <name>

(Same shape.)

### Option C — <name>

(Same shape, when applicable.)

## Benchmark

Apply WHAT/WHY/HOW/SIMULATE from `benchmark-methodology`.

- **WHAT** — Which company solved a similar problem? Be specific (not
  "Stripe is good at APIs" — "Stripe collapsed signup to 7 lines of code in
  2011 to match developer time-to-first-success").
- **WHY** — The structural reason their approach worked.
- **HOW** — Translation to Packlinx's stage, market, solo-operator economics.
- **SIMULATE** — Expected outcome, primary failure mode, kill criterion.

If no precedent exists, mark **unproven** and reduce initial commitment.

## Decision

State the choice in one sentence. Then 2–4 sentences on the reasoning. The
reasoning is the audit trail; future-you will grep this.

## Consequences

- What gets easier.
- What gets harder.
- What we now have to monitor (specific metric + threshold).
- Kill criterion: at what observed signal do we revisit this ADR?

## Rollback plan

If this is one-way: state honestly that there is no rollback and what the
exit cost would be. If two-way: state the steps to undo, and how long they
take.
```

### CEO/board hand-off rules

- Reversibility one-way → CEO sign-off required before "accepted."
- Reversibility two-way + < $100/mo recurring → CTO authority, log only.
- Vendor lock-in or > $100/mo recurring → CEO sign-off, board notification.
- Mutates vendor data without tested rollback → refuse. Not negotiable.

## Part 2 — Code review checklist (Next.js 16 + Supabase + Postgres)

Apply this on every non-trivial PR. Skip checks that are clearly inapplicable;
do not skip silently — leave a one-line comment so the author knows.

### Schema and migrations

- [ ] Migration is reversible (or explicitly marked one-way with rollback
      plan in the PR description).
- [ ] No `DROP COLUMN` / `DROP TABLE` without a deprecation window.
- [ ] Backfills use batched updates, not single-shot UPDATE on large tables.
- [ ] `NOT NULL` added with default or in two-step migration (add nullable
      → backfill → set NOT NULL).
- [ ] RLS policies reviewed for the new table/column. Default deny.
- [ ] Indexes match the query patterns the PR introduces.
- [ ] No mixed-encoding text columns (utf8mb4 / utf8 across joins).

### Vendor data path

- [ ] Insert/update of vendor data has a tested rollback path.
- [ ] Source-of-truth field is logged on every mutation (who/when/why).
- [ ] No silent overwrites. If a record exists, the PR explicitly chooses
      merge / reject / replace and documents which.
- [ ] Korean text fields handled per `encoding-discipline` (NFC, no BOM).

### Auth and RLS

- [ ] Server-side checks present, not just client-side guards.
- [ ] Service-role keys never reach the browser.
- [ ] New endpoint has a written threat model paragraph (who can call it,
      what they can do, what stops abuse).
- [ ] Rate-limit applied or explicitly deferred with a tracking ticket.

### Next.js 16 specifics

- [ ] Server vs. client component boundary is intentional. No `"use client"`
      added "to make TypeScript happy."
- [ ] No unbounded `cache: "force-cache"` on data that mutates.
- [ ] `dynamic` route params are validated.
- [ ] Streaming used for slow data; loading.tsx provided where it helps.
- [ ] No accidental client bundle bloat (heavy libs imported in client
      components when a server component would do).
- [ ] Edge runtime only when the function genuinely needs it.

### Tests

- [ ] New behavior has a test that would have caught the original bug or
      verified the new feature against its DoD.
- [ ] No tests deleted or marked `.skip` without justification.
- [ ] Mocks do not bypass the data-integrity guarantees this PR is supposed
      to enforce.

### Production safety

- [ ] Feature flag or staged rollout for anything user-facing.
- [ ] Logs added for the new failure modes, not just success paths.
- [ ] Rollback steps documented in the PR description if the change touches
      production state.

### Review-comment style

- Lead with the highest-severity issue. Don't bury "this drops vendor data
  silently" under nit-level whitespace comments.
- Phrase as a question when you might be wrong: "Is this intentional?"
  Phrase as a directive when you're sure: "Change this — schema migration
  is irreversible."
- Approve only when every must-fix is addressed, not when the author is
  tired.

## Self-check before submitting an ADR or approving a PR

- [ ] Could a future CTO read this ADR / review and understand both the
      decision and the reasoning?
- [ ] Are the kill criterion and rollback plan concrete?
- [ ] Did the benchmark step actually translate to our stage, or did it stop
      at "Company X does this"?
- [ ] If this is one-way, has the CEO seen the options before "accepted"?
