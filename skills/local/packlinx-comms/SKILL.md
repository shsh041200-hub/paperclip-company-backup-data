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

## Routing CEO sign-off vs board sign-off (PACAA-694)

`request_confirmation`, `ask_user_questions`, `suggest_tasks` **always
route to the board (founder) via Telegram**. The CEO cannot accept them
(401 — board-only gate). Therefore:

| Decision type | Channel |
|---|---|
| **CEO scope** — reversible ops, internal data migration, PR merge approval, option selection between reversible paths, sub-agent sign-off | **Comment escalation** on the issue thread. Format: `[ESCALATION → CEO]` prefix + tight summary + ≤3 options + your recommendation. CEO replies with sign-off comment + PATCHes status (you stay assignee, pick up the wake). |
| **Board scope** — irreversible (one-way door), budget/spend changes, external/policy commitments, hiring decisions, account-level access changes, board's calendar/wallet | `request_confirmation` (yes/no), `ask_user_questions` (option select), `suggest_tasks` (task pick). |

**Rule of thumb:** if the action is reversible and contained within
Packlinx's internal systems (DB row UPDATE, code merge, slug rename,
content edit, scope re-route), route to the **CEO via comment**. If the
action crosses a one-way door, spends money, or touches the founder's
account/calendar, route to the **board via interaction**.

**Anti-pattern (5 cases logged 2026-05-13~14, PACAA-681/682/688/691):**
Sub-agent creates `request_confirmation` "for CEO approval." Board sees
it via Telegram, no DELETE endpoint exists (`feedback_no_interaction_
cancel_endpoint`), board's queue accumulates noise, CEO is 401 on
accept, and the CEO has to comment-route the decision anyway. Always
comment-route CEO scope from the start.

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
- [ ] **If creating an interaction (`request_confirmation`,
      `ask_user_questions`, `suggest_tasks`): the decision is truly
      board-scope (one-way door / spend / external commitment).** For
      CEO-scope decisions (reversible / internal / PR merge / option
      pick) → comment-route only, no interaction. See routing section
      above.

***

## Board-facing Telegram output (PACAA-106 + PACAA-311)

Telegram alerts to the board (대표) follow a fixed three-class shape.
Anything sent through `tools/board-visibility/notify-telegram.py` is
built by `_telegram_format` and validated by `assert_telegram_safe`
before fire. Do not hand-format Telegram bodies that bypass the
builders.

### PACAA-311 — "send only when action is required" gate

Board directive 2026-05-08: 봇 보고는 보드의 행동이 꼭 필요할 때만
보내고, 보낼 때는 "현재 X 작업중인데 보드님의 Y 행동이 필요합니다"
형태로 작성한다. 요약-말줄임("...") 금지 — 보드가 내용을 모르면
선택·승인 자체가 의미가 없다.

Before creating any interaction (`request_confirmation`,
`ask_user_questions`, `suggest_tasks`) or approval, the author must
satisfy the **send gate**:

- Is a concrete board action required (✅/❌, 옵션 N 중 1, 자유 답장,
  외부 대시보드 클릭)?
- 가능한 **YES** → 만들어 보내기 OK.
- 가능한 **NO** (FYI / 관찰 / 진행 보고 / 인지 요청) → 만들지 말 것.
  내부 메모는 PARA / Journal / decision log, 진행 상황은 issue
  comment 만 사용. Telegram 으로는 절대 보내지 않는다.

The `feedback_board_fyi_silent_response` memory ("보드 FYI / observation
은 silent action") is the same rule — PACAA-311 hardens it for any
Paperclip-bot surface.

### "현재 작업 / 보드님 필요 행동" frame

Every Telegram body opens with this two-line frame in Korean,
regardless of class:

```
현재 작업: {한 줄 — 무슨 일을 하고 있는지, 사실 기반}
보드님 필요 행동: {한 줄 — 무엇을 결정/입력/클릭해야 하는지}
```

Then the class-specific body block (A/B/C) follows.

### Tone — 전문가가 초보자에게 설명하듯

Write as a domain expert calmly briefing a capable but
non-specialist board member:

- Define unfamiliar terms inline ("rate limit" → "Vercel 호출
  횟수가 한도를 넘어 30분간 차단됨").
- Spell out implications ("배포 실패" → "사이트가 1시간 동안 옛 버전
  유지").
- State the recommendation + 1-line rationale BEFORE the options.
- Translate internal jargon ("backlog", "deferred", "P1", "in_review")
  into plain Korean.

### Brief but complete — no ellipsis truncation

The body must contain enough context for the board to decide WITHOUT
opening the attachment. **Mid-sentence ellipsis (`...`, `…`,
`(이하 생략)`) is BANNED** — it hides exactly the content the board
needs. If a section won't fit:

- Shorten the source content (stronger summarization, not
  truncation), or
- Split into a second attachment (`{IDENTIFIER}_{kind}_part2_*.txt`),
  or
- Move secondary detail into the issue comment thread and link to it.

### Three classes (templates updated PACAA-311)

**A. 액션** — board needs to do something off-platform.

```
현재 작업: {한 줄}
보드님 필요 행동: {한 줄 — 어디서 무엇을 클릭/입력}

배경: {2~3줄 — 왜 보드가 직접 해야 하는지}
세부 절차:
1) {UI text label 까지 명시한 step}
2) {step}
3) {step}
완료 신호: {보드가 무엇을 보면 "끝"이라고 판단할 수 있는지}
상세: {첨부 파일명}
```

**B. 승인** — yes/no decision. Inline buttons: `✅ 승인` / `❌ 반려`.

```
현재 작업: {한 줄}
보드님 필요 행동: 아래 결정에 ✅승인 또는 ❌반려

제안: {한 줄 — 무엇을 하려는지}
근거: {2~3줄 — 왜 이 길이 옳은지, 측정 가능한 근거 우선}
승인 시: {2~3줄 — 다음 단계 + 비용 + 되돌릴 수 있는지}
반려 시: {2~3줄 — 멈추거나 대안 경로}
상세: {첨부 파일명}
```

**C. 선택** — pick one of N options. ≤3 options → inline buttons.
>3 → "1, 2, 3 중 답장해 주세요" hint + numeric reply.

```
현재 작업: {한 줄}
보드님 필요 행동: 아래 N개 옵션 중 하나 선택

상황: {2~3줄 — 왜 갈림길인지}
1) {선택지 1}
   영향: {2줄 — 비용/시간/되돌리기 가능 여부}
2) {선택지 2}
   영향: {2줄}
3) {선택지 3}
   영향: {2줄}

⭐ 추천: {번호}
근거: {2~3줄 — 왜 이게 추천인지}
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
| `issues?status=in_review` | **send gate FAIL — do not push.** |

`in_review` 묶음은 PACAA-311 send-gate 를 통과하지 못한다 (보드 즉시
행동 요구 아님). bot 으로는 보내지 않고, 보드가 자발적으로 대시보드를
열 때만 노출한다.

### Readability rules (enforced by `assert_telegram_safe`)

1. **Send gate.** Reject if source is non-actionable (FYI /
   observation / status-only / `in_review` bundle).
2. **Korean first.** Body Korean ≥ 70% of tokens (proper-noun
   whitelist excluded: Vercel, Cloudflare, Naver, etc.).
3. **Frame opener.** Body MUST start with "현재 작업:" line and have
   "보드님 필요 행동:" within the first 3 lines.
4. **No ellipsis.** Body and attachment may not contain `...`, `…`,
   or `(이하 생략)` as truncation markers (literal `…` inside Korean
   prose like "그래서…" is banned too — rephrase).
5. Plain words ("임계값" → "이 숫자에 도달함").
6. ≤1 PACAA-XX in body.
7. Mobile width: ≤25 Korean chars per line; no boxes; no
   `═──━│` divider clutter; short button labels.
8. Functional emojis only: ⭐ (추천), ✅ (승인), ❌ (반려). No
   decorative emojis anywhere.

### Attachment

Filename: `{IDENTIFIER}_{kind}_{YYYYMMDD-HHMM}.txt`
(kind ∈ `action|approval|choice`). `non_actionable` is removed —
those are gated out at send time.

Sections (only the present ones, in this order):
`■ 무엇을 결정해야 하나` → `■ 배경 (왜 지금)` →
`■ 권장 / 선택지` → `■ 위험 / 이 일이 안 되면` →
`■ 직전 대화`.

Indent depth ≤1 (2 spaces or `- `). No box characters.
**Length cap 4000 chars.** Source longer than 4000 → split into
`part2_*.txt`, never truncate with `…(이하 생략)` (PACAA-311).

### Tooling

- `notify-telegram.py --sample={action|approval|choice}` — synthesize
  one fixture through the builder pipeline. Use to verify formatting
  without waiting for a live event.
- `notify-telegram.py --dry-run` — print body+attachment for every
  pending approval/interaction; no Telegram fire.
- `assert_telegram_safe(body, attachment, kind)` — raises
  `TelegramFormatViolation` on any rule break. Called automatically
  inside `notify-telegram.py main()`; dry-run reports without raising.
