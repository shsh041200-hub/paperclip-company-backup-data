---
name: "PACAA-7.1 — Define and write company common skill set"
assignee: "ceo"
---

Define the canonical set of company-wide skills that every Packlinx agent receives at hire.

## Scope

- Audit the existing 3 company skills: `encoding-discipline`, `packlinx-context`, `benchmark-methodology`.
- Decide which Paperclip-bundled skills every agent needs (`paperclip`, `para-memory-files`, etc.).
- Identify gaps: what skill should every agent have that doesn't exist yet (e.g., `packlinx-comms`, `packlinx-decision-log`)?
- Write any missing common skills.
- Produce a single canonical list `desiredSkills.common[]` to be referenced by every hire.

## Out of scope

- Per-role specialized skills (covered by [PACAA-7.3](/PACAA/issues/PACAA-7.3))

## Definition of done

- Updated/new SKILL.md files committed under `skills/d5e183da-.../<slug>/`
- Canonical desiredSkills list documented in PACAA-7's plan or a follow-up doc
- Skills installed via `POST /api/companies/{companyId}/skills/import` and verified in API response
