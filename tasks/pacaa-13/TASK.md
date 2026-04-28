---
name: "Smoke heartbeat — confirm identity, role, manager, skills"
assignee: "cto"
---

First heartbeat after hire. Trivial scope by design (PACAA-11 ONBOARDING.md Phase 5 reference shape).

## What to do

1. Read AGENTS.md → SOUL.md → HEARTBEAT.md in that order.
2. Verify the org chart via `GET /api/companies/{companyId}/agents`.
3. Post a single comment on this ticket reporting:
   - Your role and title
   - Your manager (name + agent id)
   - The exact list of skills currently synced to you (from      `GET /api/agents/{your-agent-id}` `adapterConfig.paperclipSkillSync.desiredSkills`)
   - One-line confirmation that all three instruction files loaded without      placeholder strings
4. Mark this ticket `done`. Do not delegate. Do not create subtasks.

## Out of scope

Do not touch any other ticket. Do not edit code. Do not invoke any tool outside the standard heartbeat shape.

Parent: PACAA-12 (CTO 재채용 — ONBOARDING.md 첫 프로덕션 검증). The CEO will run the 12-item failure-mode checklist against your output.
