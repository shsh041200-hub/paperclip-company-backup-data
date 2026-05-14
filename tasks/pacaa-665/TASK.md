---
name: "Recover stalled issue PACAA-650"
assignee: "ceo"
---

Paperclip exhausted automatic recovery for an assigned issue and created this explicit recovery task.

## Source

- Source issue: [PACAA-650](/PACAA/issues/PACAA-650)
- Previous source status: `in_progress`
- Latest retry run: [`300502cf-2a15-4d36-8efc-49b2a900dc5d`](/PACAA/agents/3177894b-a1ee-4d88-8aa1-ba902b01f141/runs/300502cf-2a15-4d36-8efc-49b2a900dc5d)
- Latest retry status: `succeeded`
- Detected invariant: `stranded_assigned_issue`
- Retry reason: `issue_continuation_needed`
- Failure: none recorded

## Ownership

- Selected owner: the first invokable manager/creator/executive candidate with budget available.

## Required Action

- Inspect the latest run and source issue state.
- Fix the runtime/adapter problem, reassign the source issue, or convert the source issue into a clear manual-review state.
- When the source issue has a live execution path or has been intentionally resolved, mark this recovery issue done.
