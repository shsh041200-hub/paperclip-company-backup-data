---
name: "[CTO] PACAA-828 enforcement 확장: legacy /api/approvals = CEO-only (request_board_approval)"
assignee: "ceo"
---

갭: PACAA-830 은 /api/issues/{id}/interactions 3종만 게이트. /api/companies/{cid}/approvals 의 request_board_approval 은 미게이트 — sub-agent 가 자유 발의, notify-telegram check_pending_approvals 가 보드 텔레그램. 실사례 2026-05-19: BE agent 가 PACAA-751 f5501a60 발의, CEO a043b03c 와 중복. Deliverable: approvals POST 동일 가드 + 정책 문서 4채널 확장. Acceptance: sub-agent 토큰 POST 403 / CEO 200 / 정책 grep 4채널. Priority medium.
