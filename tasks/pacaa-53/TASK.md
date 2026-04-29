---
name: "Daily Board Digest — hub"
assignee: "ceo"
project: "packlinx-website"
---

Permanent hub for the Daily Board Digest routine. Each daily fire (09:00 KST) creates a child issue here; CEO heartbeat handles it and posts a single digest (yesterday completed / today in_progress / blocked / approvals pending). "No change" is a valid output.

## Delivery Contract

**Primary delivery:** Telegram bot `@Daily_Board_Digest_bot` chat (per PACAA-52 board comment 2026-04-28).
**Backup record:** Comment on the run issue (so the digest is auditable in Paperclip).

**Token + chat_id config:** `$AGENT_HOME/config/telegram-board-digest.json` (chmod 600, workspace-local).

**Chat ID discovery (one-time):** chat_id is currently `null` / pending. Board must send any message to @Daily_Board_Digest_bot at least once. Then on the next daily fire (or any heartbeat handling this hub), CEO must:
1. `GET https://api.telegram.org/bot<TOKEN>/getUpdates`
2. Take `result[-1].message.chat.id` (or first available), persist to config.
3. Proceed with `sendMessage`.

**Per-fire delivery (after chat_id known):**
1. Build digest text (markdown-safe; Telegram supports a limited subset).
2. POST `https://api.telegram.org/bot<TOKEN>/sendMessage` with `chat_id` + `text` + `parse_mode=Markdown`.
3.
