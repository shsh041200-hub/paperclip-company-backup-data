---
name: "event-driven-orchestration"
description: "Required deadline-discipline protocol for every Packlinx agent. Before setting any time-based deadline on a task, classify it as Category A (externally time-bound) or Category B (event-bound) and convert Category B to event triggers. Used at task creation, plan authoring, and during stall reflection."
slug: "event-driven-orchestration"
metadata:
  paperclip:
    slug: "event-driven-orchestration"
    skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
  paperclipSkillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
  skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
key: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
---

# Event-driven Orchestration — Packlinx operating paradigm

Packlinx is an **AI-agent company**. Applying human-company time-based assumptions verbatim turns work that finishes in 30 minutes into a system that thinks the deadline is 3 days away — chained tasks that should take 1.5 hours stretch to a full week. This skill is the **deadline-classification + trigger-chain** protocol that prevents that loss.

The authority for this skill is the PACAA-146 board directive (2026-05-01).

## When to invoke

**Mandatory invocation:**

1. Creating a new task / issue / child issue — pass the self-question check before setting `dueAt` or a deadline in the body.
2. Authoring a plan document — every Project Goal / phase / milestone must be classified.
3. Converting a board / user message into a task — do not transcribe human phrasing like "within X days" verbatim.
4. During heartbeat stall reflection — reclassify time-bound backlog/blocked items as Category B candidates.
5. When applying generic business knowledge — when defaults like "sprint", "quarterly OKR", or "weekly 1:1" surface, run them through the conversion dictionary first.

**Skippable:** simple routing, acks, follow-up steps of already-classified-and-approved work.

## Self-question (mandatory)

Right before setting a deadline, answer in one line:

> **"Does this deadline really depend on time, or does it depend on the completion of a prior task / event?"**

If the latter, do not set a time deadline — define a **trigger condition** instead.

## Two categories

### Category A — Time-based justified

Four reasons that justify a time-based deadline. Anything else is B.

1. **External dependency** — a delay we cannot control. Examples: Google indexing 12 weeks, Vercel response 36h, GSC data reprocessing 48h, Kakao / Naver API quota refresh.
2. **Data accumulation** — a measurement that is meaningful only after a window. Examples: WUV baseline 1 week, monthly user behaviour, quarterly cohort retention.
3. **External commitment / event** — a commitment we made to an outside party. Examples: quarterly report, investor meeting, contract expiry, statutory filing deadline.
4. **Natural market cycle** — the industry's intrinsic time. Examples: Korean packaging peak season (Sep–Nov), Korean holiday closures, fiscal year.

If a deadline matches one of these four, keep the time deadline but apply **Principle 4** (deadline redefinition).

### Category B — Event-based justified

Time deadlines on the following work types are **almost always false**. Convert to triggers.

* **Production** — code implementation, design output, content writing, document drafting.
* **Verification** — code review, QA, hypothesis validation, test execution.
* **Decisions** — ADR drafting, option comparison, board approval requests.
* **Learning / retrospective** — retros, decision audits, post-mortems.

The real dependency for these is "previous step done" or "decision input arrived." "Within 3 days" is just calendar pressure mimicked from human companies.

## Four operating principles

### Principle 1 — Separate the two categories (definitions above)

When defining work, label the category. State it in the body or in metadata.

### Principle 2 — Mandatory self-question

If the self-question above does not pass, do not set a time deadline. If it passes, write the specific A reason in the body in one line ("External dependency: Google indexing 12 weeks").

### Principle 3 — Automate trigger chains

When defining event-based work, bake the following 3 elements into the body / metadata:

1. **Precondition (Trigger):** which event starts this work.
   * e.g., "When PACAA-X transitions to status=done"
   * e.g., "When the board accepts plan revision N"
   * e.g., "When validation result X passes the threshold"
2. **Immediate execution:** active on trigger fire, no deadline waiting. In Paperclip, set `parentIssueId` correctly so the child-completion wake fires automatically, or rely on blocker→unblock auto-wake.
3. **Downstream notification:** wire a chained issue or routine trigger so the next task starts automatically when this one completes. No manual board wakes.

### Principle 4 — Redefine the meaning of time deadlines

Even in Category A, a time deadline is a **"check-in"**, not a "commit":

* If the work finishes early, advance immediately (do not wait for the deadline).
* If the work is not done by the deadline, reassess at that point (not auto-fail).
* `dueAt` is a _check-in_ signal, not a _commit_.

## Human → AI conversion dictionary

When the CEO and any agent apply generic business knowledge, the following conversions are mandatory. When a human-company assumption surfaces, replace it with the **AI-agent-company equivalent**.

| Human-company assumption        | AI-agent-company conversion                                         |
| ------------------------------- | ------------------------------------------------------------------- |
| "2-week sprint"                 | "Event chain + time-box only Category A items"                      |
| "Quarterly OKR"                 | "Goal tree + event triggers + Category A measurement window"        |
| "Weekly 1:1"                    | "Auto-report on trigger fire / push-on-change"                      |
| "Project Gantt chart"           | "Event-dependency graph (DAG)"                                      |
| "Resource plan"                 | "Agent concurrency + parallel child issues"                         |
| "Deadline pressure"             | "Pressure to complete the prior task"                               |
| "Daily standup"                 | "heartbeat stall reflection + active child scan"                    |
| "Quarterly review"              | "Auto-retrospective trigger when Category A measurement window ends"|
| "Off-site workshop"             | "Board alignment meeting + memo capture (event)"                    |
| "Rollout schedule"              | "Feature flag + canary + metric gate"                               |
| "Escalation SLA 4h"             | "Escalate immediately on blocker, hop-count limit"                  |

**Suspect every default that worked in a human company.** 95% are calendar-pressure mimicry; only 5% are real time dependencies.

## Paperclip application pattern

How to actually wire this on Paperclip:

1. **State the category in the issue body header.** Example:

   ```text
   ## Deadline classification
   - Category: B (production work)
   - Trigger: PACAA-95 status=done
   - Downstream: PACAA-104 auto-wake (parentIssueId set)
   ```

2. **`dueAt` rules.** Set `dueAt` only on Category A. For Category B, leave `dueAt` empty and state the trigger condition in the body.

3. **`parentIssueId` is mandatory.** Always set it on child-issue creation so `issue_children_completed` wake fires automatically.

4. **If you find a Category B issue with `dueAt` set** — during stall reflection, PATCH it to clear `dueAt` and add the trigger statement. No board approval needed (operational correction, not a change of intent).

5. **Even Category A: if the work finished early, advance immediately** — do not wait for `dueAt`. If the next task's trigger is wired as "PACAA-X done", it fires the moment the prior issue is marked done.

## Anti-patterns

* **Transcribing human phrases like "within 3 days" verbatim.** Even if the board / user used the phrase, the conversion duty falls on the agent. Self-question first, then answer.
* **Setting `dueAt` without writing the trigger.** Even Category A items can have a trigger (e.g., "after GSC data reprocessing completes"). State both.
* **Pacing event work by the calendar.** Human-sprint defaults like "let it run for a week even if the diff is small" are a pure loss for AI agents.
* **Manually firing trigger chains.** Do not make the board press wake every time. Automate via `parentIssueId` / `blockedByIssueIds`.
* **Inventing Category A reasons.** Don't justify time-boxing as "external dependency" when there is no real external blocker. If it does not match one of the four reasons, it's B.

## Self-check (right before setting a deadline)

- [ ] Self-question answered: time-dependent / event-dependent
- [ ] Category label stated in the body
- [ ] If B, trigger + downstream notification stated; `dueAt` cleared
- [ ] If A, the specific reason among the 4 stated; `dueAt` is a _check-in_
- [ ] Auto-wake chain wired via `parentIssueId` / `blockedByIssueIds`
- [ ] When using human-company assumptions (sprint, quarter, SLA), conversion dictionary applied

## Validation metrics (PACAA-146 board agreement)

One week after applying this skill, measure:

* Average task completion time (hours, not days)
* Total chain time (A → B → C) (target: hours, not a week)
* Agent idle time (target: immediate fire, not waiting)
* Among issues with `dueAt`, the share that is Category A (target ≥80%)

If metrics fall short, reinforce the skill (add anti-patterns, expand the conversion dictionary).
