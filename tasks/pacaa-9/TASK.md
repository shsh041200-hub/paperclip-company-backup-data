---
name: "PACAA-7.2 — Author SOUL.md and AGENTS.md (HEARTBEAT) standard templates"
assignee: "ceo"
---

Author the canonical SOUL.md and AGENTS.md/HEARTBEAT.md templates that every non-CEO Packlinx agent inherits at hire.

## Scope

- SOUL.md template — identity, strategic posture, role-specific philosophy slots, voice, refusal list
- AGENTS.md (entry) — short pointer file the runtime loads first
- HEARTBEAT.md template — phase-by-phase execution checklist scaled to non-CEO roles
- Korean-aware tone, English internal docs (per directive)
- Token-efficient (cap SOUL ~250 lines, HEARTBEAT ~120 lines)

## Reference materials

- CEO's existing SOUL.md and HEARTBEAT.md (proven in production heartbeats)
- Stripe/Linear/Anthropic role-template patterns from the benchmark filter

## Definition of done

- Templates checked into a canonical location (e.g., `companies/.../templates/agent/`)
- Variables (role, manager, model, capabilities) clearly marked
- One example role (CTO) instantiated end-to-end as a sanity check before bulk re-hire
