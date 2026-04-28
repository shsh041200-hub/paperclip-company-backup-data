---
name: "benchmark-methodology"
description: "WHAT/WHY/HOW/SIMULATE framework for evaluating any strategic proposal against proven precedents. Use before recommending category-level decisions."
slug: "benchmark-methodology"
metadata:
  paperclip:
    slug: "benchmark-methodology"
    skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/benchmark-methodology"
  paperclipSkillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/benchmark-methodology"
  skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/benchmark-methodology"
key: "company/d5e183da-c58f-4124-8075-493330dce4c4/benchmark-methodology"
---

# Benchmark Methodology

## When to invoke this skill

Use this skill before:

* Proposing a new feature, product direction, or business model
  change
* Recommending a process, tool, or organizational structure
* Choosing a technology stack or third-party service
* Setting pricing, packaging, or positioning
* Any decision that allocates more than a trivial amount of budget
  or time

Do not use it for trivial routing or implementation choices where a
clear pattern already exists in the codebase or design system.

## Core principle

**Benchmark what already works before inventing anything new.**

Originality is overrated when someone has already paid the tuition.
Most strategic problems have been solved by someone, somewhere, in
some industry. Your job is to find that precedent, understand why
it worked, translate it to our context, and project the outcome.

## The four-step filter

Apply these four steps in order. Skipping a step is the most common
failure mode.

### Step 1 — WHAT

Identify exactly what the reference company did. Be specific.

* Bad: "Stripe focused on developers."
* Good: "Stripe shipped a 7-line code sample on the homepage in
  2011, replaced multi-step signup with API-key issuance, and
  prioritized documentation as a product surface."

You should be able to point to a specific decision, artifact, or
behavior. Vague summaries are evidence you have not actually
understood the case.

### Step 2 — WHY

Understand the structural reason it worked for them. Strip the
surface; find the underlying advantage.

* Why did the 7-line code sample work? Because the developer
  audience evaluated tools by time-to-first-success, and Stripe
  collapsed that time from hours to minutes. The structural
  insight is "match the proof to how the buyer evaluates."

If you cannot articulate the structural reason, you are pattern-
matching, not benchmarking. Surface-level imitation will fail.

### Step 3 — HOW

Translate the approach to Packlinx's specific stage, resources, and
constraints. Most translation work is here.

Translate against:

* Our market (Korean B2B packaging, traditional, relationship-driven)
* Our stage (early, pre-revenue, solo-operated)
* Our users (procurement teams, SMB owners — not consumers)
* Our cost structure (one human + AI agents, not a team of 50)
* Our channels (Naver SEO, Google SEO, vendor word-of-mouth)

A direct copy-paste from Stripe's playbook will fail at Packlinx
because the audience and channels differ. The translation is the
real intellectual work.

### Step 4 — SIMULATE

Project the expected outcome before committing.

* What does success look like, measured in concrete numbers?
* What is the most likely failure mode?
* What is the kill criterion — at what point do we abandon this
  approach?
* What is the smallest test that could falsify the bet?

If you cannot simulate the outcome, the proposal is not ready.

## Required components of any strategic proposal

Every proposal you write must include:

1. **Precedent.** At least one company that executed a similar
   strategy. Successes count; informative failures count more.
2. **Structural reason.** Why their approach worked or failed.
3. **Translation.** How the approach adapts to Packlinx's stage
   and constraints.
4. **Risks and countermeasures.** Specific failure modes you will
   monitor.
5. **Kill criterion.** The metric and threshold at which you
   abandon the bet.

Proposals without these components should be marked "incomplete"
and returned for further work.

## Reference tiers

When choosing benchmarks:

**Tier 1 — Global category leaders.** Apple, Amazon, Google, Meta,
Stripe, Netflix, Microsoft, Nvidia. Use for high-level decision
frameworks and capital allocation patterns. Most don't apply at
our stage.

**Tier 2 — B2B marketplaces and vertical directories.** Alibaba,
Thomasnet, Kompass, Faire, Ankorstore, Houzz Pro. Structurally
similar to Packlinx. Most directly applicable.

**Tier 3 — Korean domestic plays.** 위키트, 엠파크, 이음, 오늘의집,
크몽, 네이버 스마트스토어. Reveals Korean buyer expectations and
UX conventions. Adapt for fluency; do not copy mediocre execution.

**Tier 4 — Adjacent patterns.** Linear, Notion, Stripe Docs (B2B
SaaS UI standards). Substack, Beehiiv (content-led acquisition).
Use as templates, not direct comps.

## What to avoid

* **Defaulting to first-principles.** Always check for precedent
  first. First-principles is the fallback, not the starting point.
* **Romanticizing originality.** Novelty is not a feature; it is
  a risk premium.
* **Skipping the WHY step.** Most failed copies happen here.
  Companies copy WHAT without understanding WHY.
* **Ignoring failed attempts.** A failed precedent is often more
  valuable than a success — it shows the limits of an approach.
* **Tier-1 worship.** Apple's playbook does not work for a
  pre-revenue Korean B2B directory. Match precedent to stage.

## Self-check before submitting a proposal

* [ ] Named at least one specific precedent
* [ ] Articulated the structural reason it worked or failed
* [ ] Translated explicitly to Packlinx's stage and constraints
* [ ] Defined success metric, failure mode, and kill criterion
* [ ] Smallest viable test is identified
