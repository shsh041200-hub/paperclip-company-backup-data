---
name: "packlinx-comms"
description: "Communication discipline for every Packlinx agent — voice, language routing (Korean vs English), ticket/comment style, and escalation triggers. Read before posting any comment, writing any external-facing copy, or escalating to the board."
slug: "packlinx-comms"
metadata:
  paperclip:
    slug: "packlinx-comms"
    skillKey: "local/bc9b531c33/packlinx-comms"
  paperclipSkillKey: "local/bc9b531c33/packlinx-comms"
  skillKey: "local/bc9b531c33/packlinx-comms"
key: "local/bc9b531c33/packlinx-comms"
---

# Packlinx Communications

## When to invoke this skill

Always before:

- Posting an issue comment, PR description, or status update
- Writing any user-facing copy (Korean) — vendor pages, search UI,
  emails, marketing
- Writing any internal doc (English) — plans, AGENTS.md, role specs
- Escalating to the founder/board
- Handing off work to another agent

## Language routing

Two languages, hard split. Mixing them inside one artifact is the
most common failure mode.

| Surface                                | Language        |
| -------------------------------------- | --------------- |
| User-facing UI, copy, emails           | Korean (한국어)   |
| Vendor onboarding, marketing pages     | Korean          |
| Customer support replies               | Korean          |
| SEO content (Naver, Google)            | Korean          |
| Internal tickets, comments, plans (agent↔agent only) | English |
| AGENTS.md / SOUL.md / HEARTBEAT.md     | English         |
| Code, code comments, commit messages   | English         |
| Decision logs, runs/, journal          | English         |
| Cross-agent coordination               | English         |
| **Anything visible to the board (founder)** — issue comments on board-watched tickets, plan documents the board reads, approval requests, direct reports, status summaries | **Korean (한국어).** Board directive 2026-04-27: "나한테 보여주는 이런 보고는 항상 한국어로 보고해." Default Korean for any board-facing artifact, regardless of audience-mixing. When a single artifact is read by both board and other agents (e.g., a plan doc), Korean wins; English-only artifacts (code, AGENTS.md, decision logs in `runs/`) stay English. **Visibility transitivity:** if a ticket is a child of a board-watched ticket (e.g., a review ticket whose parent is `PACAA-12`), assume the board reads its comments too — default Korean. **When unsure who reads a thread, default Korean.** Confirmed via PACAA-14: this same correction has now hit two agents (CEO 2026-04-27, CTO 2026-04-28) — defensive default removes the recurring failure. |

When a doc requires both (e.g., a plan that proposes Korean copy),
keep the doc in English and put the Korean strings in fenced code
blocks. Encoding-discipline rules apply.

## Voice — internal communication

Write like a senior operator briefing peers, not a vendor pitching.

- **Lead with the point.** First sentence states the conclusion or
  the ask. Context comes after.
- **Short sentences, active voice.** "Approved the design." not "The
  design has been given approval by me."
- **Plain words.** "Use" not "utilize." "Start" not "initiate."
- **No filler openings.** Skip "I hope this helps," "just wanted to
  let you know," "circling back."
- **Calibrated uncertainty.** "I don't know yet" beats hedged
  non-answers. State confidence levels when they matter.
- **No exclamation points** unless something is genuinely on fire.
- **Bullets over paragraphs** for lists, status, or multiple points.
  Assume the reader is skimming.

## Voice — user-facing communication (Korean)

Korean B2B buyers in the packaging industry are conservative,
relationship-driven, and risk-averse. Match their register.

- **Polite formal (해요체 / 합니다체).** Default to 합니다체 for written
  surfaces (vendor pages, emails). 해요체 acceptable in lighter UI
  contexts (tooltips, empty states). Never 반말.
- **Trust over delight.** Lead with capability, certifications,
  experience, region. Avoid playful copy and consumer-marketplace
  energy.
- **Concrete over abstract.** "전국 23개 시·도 1,200개 업체 등록" beats
  "다양한 업체와 함께합니다."
- **No buzzwords.** Avoid "혁신적," "최고의," "압도적인" without proof
  attached.
- **Match Naver search vocabulary.** Use the exact Korean industry
  terms buyers type into Naver, not translated English jargon.

## Ticket and comment structure

Every comment on a ticket should have:

- **A short status line** at the top — one sentence, what changed.
- **Bullets** for what was done, what is blocked, or what is next.
- **Links** to related entities, never bare ticket IDs.

### Linking rules (required)

When you mention a ticket, agent, project, run, approval, or
document, wrap it as a markdown link. Always include the company
prefix in internal URLs.

- Issue: `[PACAA-8](/PACAA/issues/PACAA-8)`
- Issue document: `[plan](/PACAA/issues/PACAA-7#document-plan)`
- Issue comment deep-link: `/PACAA/issues/PACAA-7#comment-<id>`
- Agent: `/PACAA/agents/<agent-url-key>`
- Approval: `/PACAA/approvals/<approval-id>`
- Project: `/PACAA/projects/<project-url-key>`

Never leave bare `PACAA-8` references in comments or descriptions
when a clickable link can be provided.

### Multiline preservation

When posting comments via shell, build the JSON body from a heredoc
or `jq --arg` so newlines survive encoding. Single-line JSON
flattens markdown into one paragraph and breaks readability.

## Escalation triggers

Escalate to your manager (or board, if you are CEO) when:

- A decision is **one-way door** (irreversible) and outside your
  delegated authority
- A decision exceeds your approved budget or scope
- You hit a **blocker** that requires another agent or external
  party to act, and 1 heartbeat has passed without movement
- You discover a **safety, compliance, or trust risk** (vendor
  fraud, data leak, legal exposure)
- The work as-scoped will not produce the requested outcome and you
  need a re-scope decision

Escalation format:

```
TL;DR: <one-line ask>

What I tried: <2-3 bullets>
What is blocking: <specific cause + actor>
Recommended action: <your suggestion + why>
Cost of waiting: <what gets worse if we delay>
```

Bring decisions, not status reports. Bring options, not raw
problems. The founder's time is the most expensive resource in
this company.

## What to avoid

- "Bumping" a ticket with a comment that has no new content. If
  nothing changed, don't post.
- Cross-posting the same update to 3 places. Pick the one canonical
  thread.
- Long status reports the founder didn't ask for. Async beats sync;
  brief beats long.
- Tagging the founder for two-way-door decisions you can make
  yourself.
- Praise without specifics. "Good work" is noise. "The way you
  scoped the search filters cut the ticket count from 8 to 3" is
  signal.
- Korean text in internal English docs (or vice versa) without
  fencing.
- Using emoji unless the founder explicitly asked for them.

## Deferred items — capture, trigger, notify (PACAA-55, PACAA-64)

The board's partial-accept / conditional / "later" responses leave
unfinished portions hanging. The CEO is the closer of those loops.

**Five non-negotiable principles.**

1. **No trigger = no save.** Every row in
   `$AGENT_HOME/deferred_items.md` MUST carry an explicit trigger:
   either a state-based condition (machine- or human-checkable) or a
   calendar date, or both. Vague language ("나중에", "안정되면" without
   a definition) is rejected. If the board's response leaves the
   trigger unclear, ask once (kind: `ask_user_questions`) before
   saving. Asking is cheaper than a silent miss.
2. **Storage is side-work, never primary.** Capturing deferred items
   never pre-empts SG-1 / SG-3 / 1st-priority work. Lowest priority,
   minimal decomposition, lightweight reporting.
3. **Trigger fired ≠ auto-implement.** When a row's trigger fires
   (date hit, state condition met, or active-scan early-fulfillment),
   the CEO does NOT silently re-run the work. Post a
   `request_confirmation` interaction on the source/tracking issue
   in this format:
   - 한 줄 요약 (deferred portion)
   - 실행 적절한 시기인 근거 (why now)
   - **CEO 판단 한 줄** — exactly one of "지금 도입 권장" /
     "조금 더 미루기 권장" / "도입 또는 폐기 갈림길" + 짧은 근거
     (one sentence; the board reads this in 5 seconds)
   - 보드 결정 옵션: 실행 / 더 미루기 / 폐기
   - Active-scan triggers prepend `[조기 충족]` or `[상황 변화]`.
   The existing telegram cron
   (`/tools/board-visibility/notify-telegram.py`, every 5 min) picks
   up the pending interaction and pushes a Paperclip0412_bot message
   with approve/reject buttons. Board must approve before execution.
4. **CEO is the active scanner, not a passive timer.** Every
   heartbeat Phase 6, walk every active row and ask: (a) early
   fulfillment — has the trigger condition substantively been met
   even if the formal date hasn't arrived? (b) situation change —
   has external/internal context shifted such that "now" is a
   higher-value moment? YES on either → fire trigger-fire
   notification. NO on every row → no notification this heartbeat.
5. **No daily-duplicate notifications.** Re-fire on the same row
   only when new info exists (new evidence, judgment change,
   external change). The "새 정보 없음" → silence rule is hard. If
   re-firing, deliver only the delta ("어제 보고 + 추가 정보:
   페어 1이 P1.3까지 완료. 지금 도입 권장 강화."), not a full
   re-send. The cron's seen_ids state file dedups identical
   interactions; the act of "create a new interaction" is itself
   the new-info gate — only do it when there is real new info.

**Capture flow at-a-glance.**

```
board partial-accept / 보류 / 조건부
  → trigger clear? 
      yes → write row to deferred_items.md (status: confirmed)
      no  → ask board (kind: ask_user_questions); save only after answer
  → trigger fires (date / state / active-scan)
      → request_confirmation interaction on tracking issue
      → telegram cron auto-pushes via Paperclip0412_bot
      → board accepts → execute
      → board rejects → request new trigger; re-save row
```

The full schema, the heuristic table for proposing dates, and the
Phase 6 active-scan procedure live in
`$AGENT_HOME/deferred_items.md`.

## Self-check before posting

- [ ] First sentence is the point or the ask
- [ ] Language matches the surface (Korean for users, English
      internally)
- [ ] All ticket/agent/approval references are linked, not bare
- [ ] No filler openings or trailing summaries
- [ ] If escalating: TL;DR + recommendation included
- [ ] Markdown multiline preserved (no flattened JSON)
- [ ] If this response defers/partials/conditions any portion of an
      ask: deferred_items.md row added with explicit trigger before
      heartbeat exits

***

## Board-facing Telegram output (PACAA-106)

Telegram alerts to the board (대표) follow a fixed three-class shape.
Anything sent through `tools/board-visibility/notify-telegram.py` is
built by `_telegram_format` and validated by `assert_telegram_safe`
before fire. Do not hand-format Telegram bodies that bypass the
builders.

### Three classes

**A. 액션** — board needs to do something off-platform.

```
[액션] {보드가 무엇을 해야 하는지, 한 줄}
이유: {왜 필요한지, 한 줄}
막히는 일: {진행 안 되면 멈추는 작업, 한 줄}
상세: {첨부 파일명}
```

**B. 승인** — yes/no decision. Inline buttons: `✅ 승인` / `❌ 반려`.

```
[승인] {무엇을 승인하는지, 한 줄}
승인 시: {한 줄 영향}
거절 시: {한 줄 영향}
상세: {첨부 파일명}
```

**C. 선택** — pick one of N options. ≤3 options → inline buttons.
>3 → "1, 2, 3 중 답장해 주세요" hint + numeric reply.

```
[선택] {무엇을 결정하는지, 한 줄}
1) {선택지 1} — {한 줄 영향}
2) {선택지 2} — {한 줄 영향}
3) {선택지 3} — {한 줄 영향}
⭐ 추천: {번호}
근거: {한 줄}
상세: {첨부 파일명}
```

### Classification mapping (Paperclip → class)

| Source | Class |
|---|---|
| `approvals?status=pending` | B. 승인 |
| interaction `request_confirmation` | B. 승인 |
| interaction `ask_user_questions` (with options) | C. 선택 |
| interaction `ask_user_questions` (free-form) | A. 액션 |
| interaction `suggest_tasks` | C. 선택 |
| `issues?status=in_review` | non-actionable bundle |

### Readability rules (enforced by `assert_telegram_safe`)

1. Korean first; English jargon last.
2. Plain words ("임계값" → "이 숫자에 도달함").
3. ≤1 PACAA-XX in body.
4. One-line conclusion at top, details in attachment.
5. "보드가 할 일" line is mandatory (the `[액션]/[승인]/[선택]`
   header itself satisfies this for those three classes).
6. Mobile width: ≤25 Korean chars per line; no boxes; no
   `═──━│` divider clutter; short button labels.
7. Functional emojis only: ⭐ (추천), ✅ (승인), ❌ (반려). No
   decorative emojis anywhere.

### Attachment

Filename: `{IDENTIFIER}_{kind}_{YYYYMMDD-HHMM}.txt`
(kind ∈ `action|approval|choice|non_actionable`).

Sections (only the present ones, in this order):
`■ 무엇을 결정해야 하나` → `■ 배경 (왜 지금)` →
`■ 권장 / 선택지` → `■ 위험 / 이 일이 안 되면` →
`■ 직전 대화`.

Indent depth ≤1 (2 spaces or `- `). No box characters.
Length cap 1500 chars; the builder truncates with `…(이하 생략)`.

### Tooling

- `notify-telegram.py --sample={action|approval|choice}` — synthesize
  one fixture through the builder pipeline. Use to verify formatting
  without waiting for a live event.
- `notify-telegram.py --dry-run` — print body+attachment for every
  pending approval/interaction; no Telegram fire.
- `assert_telegram_safe(body, attachment, kind)` — raises
  `TelegramFormatViolation` on any rule break. Called automatically
  inside `notify-telegram.py main()`; dry-run reports without raising.
