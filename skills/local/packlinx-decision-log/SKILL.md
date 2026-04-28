---
name: "packlinx-decision-log"
description: "Required reasoning protocol for any non-trivial decision at Packlinx — options, benchmark, decision, reversibility. Mandatory before allocating budget, hiring, committing the company to a direction, or shipping any user-facing change."
slug: "packlinx-decision-log"
metadata:
  paperclip:
    slug: "packlinx-decision-log"
    skillKey: "local/bcc6a51c5f/packlinx-decision-log"
  paperclipSkillKey: "local/bcc6a51c5f/packlinx-decision-log"
  skillKey: "local/bcc6a51c5f/packlinx-decision-log"
key: "local/bcc6a51c5f/packlinx-decision-log"
---

# Packlinx Decision Log

## When to invoke this skill

Write a decision log entry **before acting** when the work:

- Allocates more than a trivial amount of budget or agent time
- Affects user-facing surfaces (vendor pages, search, copy, SEO)
- Commits the company to a direction (vendor onboarding model,
  pricing, partnerships, hiring)
- Touches data integrity (vendor records, schema, dedup logic)
- Is a one-way door — irreversible without significant cost

**Skip the log only for trivial routing**: acknowledgments, simple
hand-offs, status updates, applying decisions already logged
elsewhere.

When in doubt, log it. The marginal cost is two minutes of writing.
The marginal benefit is a coherent audit trail that compounds across
heartbeats.

## Why this exists

Without logged reasoning, every heartbeat re-debates the same
decisions, the founder cannot audit agent judgment, and bad calls
go undiagnosed because nobody remembers the alternative options
that were rejected.

A good decision log lets a future agent (or the founder) reconstruct
**why** a choice was made — not just what was done. Code shows
what; logs show why.

## Required fields

Every decision log entry must contain these six fields. Missing
fields make the entry incomplete; mark such entries `WIP` and
return for completion.

### 1. Ticket

Issue ID (linked) and a one-line summary. Example:

> [PACAA-8](/PACAA/issues/PACAA-8) — Define and write company
> common skill set.

### 2. Goal ancestry

Which company Goal does this ladder up to? Walk up parents until
you hit a company-level Goal. If you cannot find one, the ticket
is suspect — flag it as goal-hygiene cleanup. Example:

> Parent: PACAA-7 → Phase 1 of org reset. No `goalId` set on
> either; flagging.

### 3. Options considered

**At least two** distinct options. A single option is not a
decision; it is a default. For each option:

- One-line description
- Cost / risk / reason for rejection or selection

Example:

> 1. Minimal 3-skill set. Cheapest tokens. Reject — agents lose
>    reasoning frameworks.
> 2. Maximal 11-skill set. Comprehensive. Reject — token bloat
>    every heartbeat.
> 3. Targeted 7-skill core. Chosen — covers context, discipline,
>    framework, platform without redundancy.

### 4. Benchmark

Apply the WHAT/WHY/HOW/SIMULATE filter from `benchmark-methodology`:

- **WHAT** — exactly what proven company did
- **WHY** — structural reason it worked
- **HOW** — translation to Packlinx's stage and constraints
- **SIMULATE** — projected outcome, failure mode, kill criterion

If no precedent exists for this decision, label it **"unproven"**
and **reduce the initial commitment** — smaller bet, faster
feedback, earlier kill criterion.

### 5. Decision + reasoning

One or two sentences. The chosen option plus the structural
reason it beat the alternatives. The reasoning is the audit
trail — keep it specific and falsifiable.

### 6. Reversibility

Two-way door or one-way door?

- **Two-way door**: cheap to undo. Move fast. Document and ship.
- **One-way door**: hard or impossible to undo. Slow down.
  Require board input if the decision exceeds your delegated
  authority.

State the reversibility explicitly. "Reversible by removing the
config flag" vs. "Irreversible — vendor records will be merged
permanently."

## Where decision logs live

- **Per-heartbeat decisions:** `$AGENT_HOME/runs/YYYY-MM-DD-HHMM-decisions.md`
- **Strategic / multi-heartbeat decisions:** also referenced from
  the parent ticket's `plan` document
- **Board-facing decisions:** summarized in the approval payload
  (do not paste the full log — pull the recommendation and the
  one-way-door rationale)

Filename convention is strict: agents lose track of decisions
buried in unstructured notes. Keep one file per heartbeat per
agent, dated.

## Format template

```markdown
# Decisions log — YYYY-MM-DD HH:MM TZ heartbeat

## <TICKET-ID> — <one-line summary>

**Goal ancestry:** <parent chain to company Goal>

**Options considered:**

1. **<Option name>:** <description>. <cost/risk>. <reject reason>.
2. **<Option name>:** <description>. <cost/risk>. <reject reason>.
3. **<Option name>:** <description>. <cost/risk>. CHOSEN.

**Benchmark:** <WHAT>. <WHY>. <HOW>. <SIMULATE>.

**Decision + reasoning:** <one or two sentences>.

**Reversibility:** <two-way door | one-way door + escalation
status>.
```

## Anti-patterns

- **Single-option logs.** "I considered X and chose X." That is a
  default, not a decision. Force yourself to articulate at least
  one rejected alternative.
- **Post-hoc logs.** Writing the log after acting reverse-engineers
  reasoning to fit the action. Log before acting.
- **Vague benchmarks.** "Similar to what Stripe does." Name the
  specific Stripe decision, year, structural reason.
- **Skipping reversibility.** Most bad calls happen here. If you
  did not classify the door, you cannot escalate appropriately.
- **Logging trivia.** Routing a ticket does not need a decision
  log. Reserve logs for decisions that allocate resources or
  commit direction.
- **Logging in slack/comments instead of the runs/ file.** Comments
  are the surface; the log is the record. Both can exist; they
  serve different audiences.

## Self-check before acting

- [ ] At least two real options written down
- [ ] Benchmark with named precedent (or labeled "unproven")
- [ ] Decision + structural reasoning in 1-2 sentences
- [ ] Reversibility classified
- [ ] If one-way door and outside my authority: escalation pending
- [ ] Logged to `$AGENT_HOME/runs/YYYY-MM-DD-HHMM-decisions.md`
