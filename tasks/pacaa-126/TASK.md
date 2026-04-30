---
name: "Recover stalled issue PACAA-122"
assignee: "ceo"
---

Paperclip exhausted automatic recovery for an assigned issue and created this explicit recovery task.

## Source

- Source issue: [PACAA-122](/PACAA/issues/PACAA-122)
- Previous source status: `in_progress`
- Latest retry run: [`ff87155e-05ce-4afe-8372-ffaa9e5a5bfa`](/PACAA/agents/3177894b-a1ee-4d88-8aa1-ba902b01f141/runs/ff87155e-05ce-4afe-8372-ffaa9e5a5bfa)
- Latest retry status: `failed`
- Detected invariant: `stranded_assigned_issue`
- Retry reason: `issue_continuation_needed`
- Failure: Latest retry failure details were withheld from the issue thread; inspect the linked run for evidence.

## Ownership

- Selected owner: the first invokable manager/creator/executive candidate with budget available.

## Required Action

- Inspect the latest run and source issue state.
- Fix the runtime/adapter problem, reassign the source issue, or convert the source issue into a clear manual-review state.
- When the source issue has a live execution path or has been intentionally resolved, mark this recovery issue done.
