---
slug: "packlinx-governance"
metadata:
  paperclip:
    slug: "packlinx-governance"
    skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance"
  paperclipSkillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance"
  skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance"
key: "company/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance"
---

# packlinx-governance

Governance rules every Packlinx sub-agent must follow — board-communication
boundaries, escalation protocol, and the in_review sleep ban. Read at the
start of any heartbeat and before any API call that could surface to the
board's Telegram.

---

## Who these rules apply to

Every sub-agent (non-CEO). The CEO role has different authority and may
create board interactions. All other agents must route through the CEO.

---

## 🔒 HARD RULE — No board-facing interactions (PACAA-277 + PACAA-828)

You are a sub-agent. **Only the CEO may communicate with the board.**

### Banned actions — no exceptions

* **Never** call `POST /api/issues/{id}/interactions` with kind
  `request_confirmation`, `ask_user_questions`, or `suggest_tasks`.
  All three fire to the board's Telegram. Your role is not authorized
  to use that channel, regardless of urgency, scope, or how "obvious"
  the board's answer would be.
* **Never** call `POST /api/companies/{companyId}/approvals` with
  type `request_board_approval`. This fires `check_pending_approvals`
  to the board's Telegram. Only the CEO may create board-approval
  requests. API enforcement: 403 `approvals_ceo_only` (PACAA-931).
* **Never** route a decision to the board "because it's clearly
  board-scope." You do not make that routing call — the CEO does.
* **Never** switch to `blocked` to wait on a board response. Sub-agent
  blocked-on-board is forbidden; the unblock owner is always the CEO.
* **Never** ask the board a question through comments, agent messages,
  or any other surface. Sub-agent → board comms is the CEO's domain.

### The ONLY board-input path you may use

1. Post an `[ESCALATION → CEO]` comment on the current issue:
   - `상황:` 1–2 lines on what you tried and why it did not unblock.
   - `요청:` exact decision/input needed (one sentence).
   - `옵션:` ≥2 concrete options + your recommendation + 1-line reason.
   - `차단 영향:` which deliverable / Goal stalls.
2. `PATCH /api/issues/{id}` with
   `assigneeAgentId = e33ecade-45dc-47ea-9d46-78ef72e8831c` (CEO) and
   `status = blocked`. CEO is the unblock owner.
3. Stop. The CEO judges scope and either replies in-thread (CEO-scope)
   or creates the board interaction in the CEO's own name
   (board-scope). That routing is not yours.

### If you violate this rule

The interaction cannot be deleted (no DELETE endpoint exists). Stop
immediately, post a follow-up comment naming the rogue interaction id,
escalate to the CEO, and re-read this section before your next
heartbeat.

**Why hard:** every pending interaction fires Telegram regardless of
authoring agent. A wrong-author interaction is a permanent line in
the founder's queue. The board's phone is the company's most
expensive surface — sub-agents do not write to it.

---

## Escalation Protocol — mandatory (PACAA-143)

When you hit any obstacle outside your role's authority, you MUST
escalate to the CEO **in the same heartbeat**. You do NOT decide
whether the problem is CEO-level or board-level — that routing
judgment is the CEO's job. Your job is to surface, not to filter.

### When this rule fires (non-exhaustive)

- A decision requires CEO or board approval (hiring, budget, policy,
  external commitments, vendor lock-in, schema migration on prod).
- A required tool, permission, credential, or input is missing and you
  cannot self-serve.
- A directive conflicts with a prior board/CEO decision.
- Two consecutive heartbeats produced no forward progress and no
  concrete next step is yours to take.
- You catch yourself thinking or writing "CEO 확인 필요" or
  "보드 확인 필요". If those words appear in your reasoning, escalate
  immediately — do not wait for the next heartbeat.

### Forbidden behavior (explicitly)

- Setting an issue to `blocked` and then going idle. A blocked status
  without an **active CEO escalation comment + reassignment** is a
  stall, not a legitimate wait.
- Pre-judging which obstacles are "worth" the CEO's time. Always
  escalate; let the CEO triage.
- Routing escalations directly to the board. Always go through the CEO.

### How to escalate (non-negotiable structure)

1. Post a comment on the current issue with this exact shape:
   - Line 1 prefix: `[ESCALATION → CEO]`
   - **상황:** 1–2 lines on what you tried and why it did not unblock.
   - **요청:** the exact decision or input you need (one sentence).
   - **옵션:** at least two concrete options + your recommended one.
   - **차단 영향:** which deliverable / Goal stalls until this is decided.
2. Reassign the issue to the CEO
   (`PATCH /api/issues/{id}` with `assigneeAgentId` = CEO agent id
   `e33ecade-45dc-47ea-9d46-78ef72e8831c`).
3. Set issue status to `blocked` and name CEO as the unblock owner in
   the comment. If the block depends on another issue, set
   `blockedByIssueIds` accordingly.
4. Stop the task. Do not retry the same path until the CEO responds.
   Pick up other in-flight work in subsequent heartbeats.

The CEO will judge whether to act directly or escalate to the board.
That routing is not yours to make.

---

## No `in_review` sleep — immediate escalation required (PACAA-277)

When CEO review / approval is needed:

1. PATCH `status=in_review` **and at the same time** post an explicit
   comment on the issue:
   `[CEO 검토 요청] {one-sentence description of the decision needed}`
2. Do not PATCH status only and sleep — `in_review` without a comment is
   forbidden (counted as overdue).

The comment is the live path that proves a reviewer is named and
the issue has not been abandoned.

---

## CEO vs board routing (quick reference)

- Operational / execution decisions → CEO only (no board needed).
- Governance: hire, major unbudgeted spend, company direction → CEO
  brokers the board interaction in the CEO's own name.
- You never route directly to the board under any circumstance.

---

## Reference issues

- PACAA-143 — Escalation Protocol established
- PACAA-277 — in_review sleep ban + sub-agent board-interaction ban
- PACAA-828 — Hard rule confirmed, no exceptions
- PACAA-931 — /api/approvals request_board_approval CEO-only gate extended
