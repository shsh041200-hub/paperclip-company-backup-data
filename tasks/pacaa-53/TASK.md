---
name: "Daily Board Digest — hub"
assignee: "ceo"
project: "packlinx-website"
---

Permanent hub for the Daily Board Digest routine. Each daily fire (09:00 KST) creates a child issue here; CEO heartbeat handles it and posts a single digest (yesterday completed / today in_progress / blocked / approvals pending). "No change" is a valid output.

## Delivery Contract (개정 2026-05-25)

**Primary delivery:** Comment on the run issue (audit trail in Paperclip).
**기타 surface:** 없음.

**개정 사유:** 보드 directive 2026-05-25 (PACAA-1013) — Telegram 채널 폐기. `@Daily_Board_Digest_bot` 송출 contract + token config 의무 폐기. Routine `66234a11` 은 이미 archived (이전 archive 와 별개 사유). 본 hub 의 spec 만 정리.

**Per-fire delivery:**
1. Build digest text (markdown-safe).
2. POST comment on the run issue (always).
3. 종료.

- Routine: 66234a11-9ce8-4323-8094-93e6b9497f15 (archived)
- Source: PACAA-52#document-plan (즉시 1) — 단, Telegram delivery 조항은 PACAA-1013 보드 directive 로 폐기.
