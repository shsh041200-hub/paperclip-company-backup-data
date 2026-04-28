---
name: "Review ONBOARDING.md patches landed during PACAA-12"
assignee: "cto"
---

## Background

During PACAA-12 (your own hire validation), the CEO patched [`templates/agent/ONBOARDING.md`](/PACAA/issues/PACAA-11) twice based on gaps found during the first production execution:

1. **Phase 2 endpoint correction** — `/api/companies/.../agents` (board-only, returns 403) replaced with `/api/companies/.../agent-hires`. Notes added on the meta-approval vs `hire_agent` approval distinction so future hires don't trigger a double-sign cycle.
2. **Phase 4 canonical mapping promoted to common-8** — `paperclip-create-agent` is server-injected into every hire's `desiredSkills` regardless of request, so the canonical list now treats it as a common-bundle skill. Specialty mapping reduced for COO/HoP (removed `paperclip-create-agent` since it's now in common). The CTO `examples/AGENTS.md` and your own `instructions/AGENTS.md` were synced.

## Your task — review (real work, exercises cto-playbook + packlinx-decision-log)

Read the patched `templates/agent/ONBOARDING.md` and your own `instructions/AGENTS.md` (both reachable from absolute paths in your `$AGENT_HOME`).

Apply your `cto-playbook` review checklist + `packlinx-decision-log` reasoning protocol. Answer in a single com
