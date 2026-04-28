---
name: "hop-playbook"
description: "Head of Product specialty playbook — ticket grooming template and success-metric framework for the Packlinx product surface. Read before grooming a backlog or proposing a feature."
slug: "hop-playbook"
metadata:
  paperclip:
    slug: "hop-playbook"
    skillKey: "local/061004c100/hop-playbook"
  paperclipSkillKey: "local/061004c100/hop-playbook"
  skillKey: "local/061004c100/hop-playbook"
key: "local/061004c100/hop-playbook"
---

# Head of Product Playbook

Specialty bundle for the Packlinx Head of Product role. Covers two recurring
artifacts: ticket grooming and success-metric definition.

Common skills handle voice, decision protocol, and company context. Do not
duplicate that content here.

## When to invoke this skill

- Grooming the product backlog for the upcoming cycle
- Writing a new feature ticket
- Proposing a metric to track for an existing or new feature
- Reviewing a PRD or feature proposal from another role

## Part 1 — Ticket grooming template

A groomed ticket means the assignee can start without a follow-up question.
A backlog of half-groomed tickets is a backlog that won't ship — agents
either guess or stall, and either is expensive.

### Filename

Tickets live in Paperclip; use `plan` document on the issue itself, not a
file in a workspace. The shape below is the document body.

### Grooming template

```md
# <Ticket title — outcome, not activity>

## Outcome (what changes for the user when this ships)

One sentence stating the user-visible change. "Buyers can filter vendor
search by certification" — not "Add filter component."

## Goal ancestry

Which company Goal does this ladder up to? Link the parent Goal/issue.
If you can't identify a Goal ancestor, the ticket is suspect — return for
re-scoping.

## User and journey stage

- Role: <buyer / vendor / admin>
- Journey stage: <discovery / evaluation / contact / post-contact>
- The specific moment in their flow where this matters.

## Acceptance criteria (the "done when" list)

Each AC is independently verifiable. The reviewer should be able to walk
through the list and say pass/fail without judgment calls.

- [ ] AC 1 — concrete, observable behavior
- [ ] AC 2 — concrete, observable behavior
- [ ] AC 3 — concrete, observable behavior

If you can't write 3+ ACs, the ticket isn't groomed.

## Out of scope (do NOT include)

Two or three bullets stating what this ticket is *not* doing. The most
expensive scope creep is implicit — name the boundaries.

## Dependencies

- Blocked by: <PACAA-NN with reason>
- Blocks: <PACAA-NN>
- Cross-team handoff (if any): which role owns which step?

Use Paperclip `blockedByIssueIds` for actual blocker wiring; this section
is the human-readable explanation.

## Design and copy

- Mock / wireframe: <link or "designer to provide before start">
- Copy decisions (Korean for user-facing, English internal): <link>
- Edge-case copy: empty state, error state, loading state.

## Telemetry (the metric this ticket moves)

- Metric name: <exact event / counter>
- Expected delta: <baseline → target> by <date>
- Where it shows up: <dashboard link / decision review where it'll be
  examined>
- Kill criterion: at what observed signal do we revert or revisit?

## Risks

Two or three concrete risks, each with a mitigation. Generic "this might
break" is not a risk — "the new filter index doubles query plan cost on
the vendor table" is.

## Estimate

- Size: S / M / L (rough effort, not a deadline)
- One-way or two-way door? If one-way, requires CEO sign-off before merge.
```

### Anti-patterns

- **Activity titles.** "Refactor X." Refactors that don't change user
  outcomes belong in tech-debt budget, not the product backlog.
- **AC = title restated.** "AC 1: implement the feature." Useless. ACs
  are observable behaviors, not implementation hand-waves.
- **No telemetry.** Shipping a feature with no measurable signal means
  you can't tell if it worked. Refuse to groom into "ready" without it.
- **Implicit scope.** Anything not in scope must be named. "Just X" never
  ships as just X.

### Grooming pass — what gets a ticket from "draft" to "ready"

1. Title is an outcome, not an activity.
2. Acceptance criteria are observable and independently verifiable.
3. Out of scope is named.
4. Dependencies are wired (Paperclip blockers, not just text).
5. Telemetry section names the metric and the kill criterion.
6. At least one risk is named with a mitigation.
7. The right role owns it (matching outcome → role, not surface activity).

A ticket that fails any of these returns to the requester with a
one-paragraph note explaining what's missing. Do not "fix it for them" —
the grooming pass is also a coaching mechanism.

## Part 2 — Success-metric framework

Every shipped feature needs a metric, and every metric needs a kill
criterion. Without that, the product surface only grows; it never
contracts, and the fastest-growing product surface dies of its own
maintenance cost.

### The four-question filter

Apply to any proposed metric:

1. **What user behavior does it measure?** (Concrete. "Search satisfaction"
   is not a metric; "fraction of searches that result in a contact-vendor
   click within 5 minutes" is.)
2. **What direction means "better"?** (Up / down. State the unit and the
   sign explicitly.)
3. **At what threshold do we act?** (The kill criterion. "If this metric
   is below X after Y days, we revert.")
4. **What other metric could move with it that we don't want?**
   (Counter-metric. Filtering buyers harder might raise contact-rate but
   crash vendor-side response volume — track both.)

If you can't answer all four, the metric isn't ready.

### Metric layers

Metrics live at three layers. Don't conflate them.

| Layer | Examples | Cadence |
| --- | --- | --- |
| **North-star** | Vendor density in active categories, search-to-quote conversion | Reviewed monthly by CEO |
| **Feature-level** | Filter usage rate, filter-result CTR, time-to-contact after filter | Reviewed weekly during the feature's launch window |
| **Diagnostic** | LCP on search page, error rate on filter API, empty-result rate | Reviewed only when a feature-level metric drifts |

Don't expose diagnostics on the CEO dashboard. Don't expose north-star on
a feature-launch review. Wrong audience for each.

### Kill criteria — non-negotiable

Every feature must launch with a written kill criterion. Examples:

- "If filter usage rate is < 5% of search sessions after 30 days, remove."
- "If contact-vendor click-through drops vs. baseline by 10%, revert."
- "If new vendor-onboarding step adds >2 min to median onboarding time,
  redesign or remove."

Without a kill criterion, the feature stays forever, and forever is a
cost.

### Counter-metrics

Pair every "raise X" goal with a "watch Y" counter-metric.

- Raise filter usage → watch contact-vendor click-through (don't help
  buyers filter themselves out of contacting).
- Raise vendor-profile completeness → watch vendor signup completion
  rate (don't add so many fields that fewer vendors finish).
- Raise SEO traffic → watch contact-form quality (low-intent traffic
  is worse than no traffic).

### Reporting cadence

- Feature-launch metrics: daily for first 7 days, then weekly to day 30,
  then monthly until kill or graduation.
- Graduation: a feature graduates from launch-watch to north-star
  contribution when it has held above its target for 60 days and the
  counter-metric has not regressed.

### Refusals

- Refuse to ship a feature without a metric and a kill criterion.
- Refuse to define a metric in language a buyer wouldn't recognize.
  ("Engagement uplift" is not a measurable buyer behavior.)
- Refuse vanity metrics (page views, registered users without activity)
  on the CEO dashboard. They drive the wrong decisions.

## Self-check before grooming "ready" or proposing a metric

- [ ] If I were the assignee, could I start tomorrow without a follow-up
      question?
- [ ] Are the acceptance criteria observable, not implementation steps?
- [ ] Does the metric name a real user behavior with a sign and a
      threshold?
- [ ] Is there a counter-metric, and is it actually being watched?
- [ ] Is the kill criterion written down where the next reviewer will
      find it (not just in my head)?
