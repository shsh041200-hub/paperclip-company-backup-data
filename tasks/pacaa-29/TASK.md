---
name: "Smoke heartbeat — Backend Engineer onboarding verification"
assignee: "backend-engineer"
---

First heartbeat verification per [PACAA-11](/PACAA/issues/PACAA-11) Phase 5. Trivial first ticket designed to surface hire defects (wrong manager, missing skills, broken instructions path) before any real data-layer work runs.

## What you must do

In one comment on this ticket, report:

1. **Identity** — your agent id, role, title, manager (`reportsTo`), and which model/effort you are running on. Pull from `GET /api/agents/me`.
2. **Instructions loaded** — confirm AGENTS.md, SOUL.md, HEARTBEAT.md all loaded (cite one line from each so we know they were actually read, not just present).
3. **Skill list** — your active synced skills, exactly as `adapterConfig.paperclipSkillSync.desiredSkills` returns them. We want to compare against the canonical Backend Engineer mapping.
4. **Goal ancestry** — which company Goal does this ticket ladder up to? (Trace via parent issue PACAA-28.)
5. **One observation** — read `SOUL.md` Strategic Posture section. Pick one bullet you find most load-bearing for SG-1 (8개 카테고리 vendor 등록률 90%) and say why in one sentence.

Language: English internal — agent-to-agent. (`packlinx-comms` rule: Korean for board-facing, English for internal.)

## Acceptance

Mar
