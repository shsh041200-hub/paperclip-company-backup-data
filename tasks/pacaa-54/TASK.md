---
name: "Stale & Blocked Issue Sweep — hub"
assignee: "ceo"
project: "packlinx-website"
---

Permanent hub for the Stale & Blocked Issue Sweep routine. Each Monday 09:00 KST fire creates a child issue here; CEO heartbeat scans and posts one report (issues with updated_at > 7d in non-terminal status / status=blocked / goalId=null orphans) with recommended unblock actions. "Clean" is a valid output.

## Delivery Contract

**Primary delivery:** Telegram bot `@Stale_Blocked_Issue_Sweep_bot` chat (per PACAA-52 board comment 2026-04-28).
**Backup record:** Comment on the run issue (audit trail in Paperclip).

**Token + chat_id config:** `$AGENT_HOME/config/telegram-stale-sweep.json` (chmod 600, workspace-local).

**Chat ID discovery (one-time):** chat_id is `null` / pending. Board must send any message to @Stale_Blocked_Issue_Sweep_bot at least once. Then on the next weekly fire (or any heartbeat handling this hub), CEO must:
1. `GET https://api.telegram.org/bot<TOKEN>/getUpdates`
2. Take `result[-1].message.chat.id`, persist to config.
3. Proceed with `sendMessage`.

**Per-fire delivery (after chat_id known):**
1. Build sweep report text (markdown-safe).
2. POST `https://api.telegram.org/bot<TOKEN>/sendMessage` with `chat_id` + `text` + `parse_mode=Markdown`.
3. On non-200, fal
