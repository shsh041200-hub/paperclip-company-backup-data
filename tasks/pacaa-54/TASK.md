---
name: "Stale & Blocked Issue Sweep — hub"
assignee: "ceo"
project: "packlinx-website"
---

Permanent hub for the Stale & Blocked Issue Sweep routine. Each Monday 09:00 KST fire creates a child issue here; CEO heartbeat scans and posts one report (issues with updated_at > 7d in non-terminal status / status=blocked / goalId=null orphans) with recommended unblock actions. "Clean" is a valid output.

## Delivery Contract (개정 2026-05-25)

**Primary delivery:** Comment on the run issue (audit trail in Paperclip).
**기타 surface:** 없음.

**개정 사유:** 보드 directive 2026-05-25 (PACAA-1013) — Telegram 채널 폐기. `@Stale_Blocked_Issue_Sweep_bot` 송출 contract + token config 의무 폐기.

**Per-fire delivery:**
1. Build sweep report text (markdown-safe).
2. POST comment on the run issue (always).
3. 종료.

- Routine: 9caeb96e-c908-4e04-ab09-a8a2359ba7c4
- Source: PACAA-52#document-plan (즉시 3) — 단, Telegram delivery 조항은 PACAA-1013 보드 directive 로 폐기.
