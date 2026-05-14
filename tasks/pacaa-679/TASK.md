---
name: "Recover stalled issue PACAA-677"
assignee: "ceo"
---

Paperclip exhausted automatic recovery for an assigned issue and created this explicit recovery task.

## Source

- Source issue: [PACAA-677](/PACAA/issues/PACAA-677)
- Previous source status: `in_progress`
- Latest retry run: [`50e37391-1d9a-4746-9d31-4c3e3454f778`](/PACAA/agents/3177894b-a1ee-4d88-8aa1-ba902b01f141/runs/50e37391-1d9a-4746-9d31-4c3e3454f778)
- Latest retry status: `cancelled`
- Detected invariant: `stranded_assigned_issue`
- Retry reason: `issue_continuation_needed`
- Failure: Latest retry failure details were withheld from the issue thread; inspect the linked run for evidence.

## Ownership

- Selected owner: the first invokable manager/creator/executive candidate with budget available.

## Required Action

- Inspect the latest run and source issue state.
- Fix the runtime/adapter problem, reassign the source issue, or convert the source issue into a clear manual-review state.
- When the source issue has a live execution path or has been intentionally resolved, mark this recovery issue done.
