---
name: "[PACAA-921 P0·P2 CTO-platform] 예산 cap + governance skill 통합 + skill lazy-load + Chrome adapter pruning"
assignee: "ceo"
---

PACAA-921 board accept 의 **CTO 플랫폼 작업** 묶음.

## D. 회사 + CEO 예산 cap (P0)
- 회사 `budgetMonthlyCents` 현재 0 (무제한). 보드 값 입력 필요.
- CEO budget 'Unlimited / No cap configured' 현재. cap 설정 + 80% soft alert 룰.
- ⚠️ CTO 발의 시 보드에 cap 값 ask_user_questions (예: 회사 50,000 cents / CEO 30,000 cents / 80% alert).

## H. governance 블록 → packlinx-governance skill 통합 (P2)
- 5개 AGENTS.md 의 HARD RULE board-facing / Escalation Protocol (PACAA-143) / No in_review sleep 블록 ~1250 단어 × 5 dedup.
- 단일 `packlinx-governance` skill 발의 + 각 AGENTS.md 는 reference 만 유지.
- LC 자문 권장 (governance 정합성).

## I. 14개 스킬 task-conditional lazy-load (P2)
- Paperclip 플랫폼이 task-conditional skill load 지원하는지 CTO 조사.
- 미지원 시: 플랫폼 PR 발의 (paperclipai repo) 또는 board escalation.
- 지원 시: 각 에이전트 skill desiredSkills 를 task tags 로 분류.

## J. Chrome adapter pruning (P2)
- 현재 6개 에이전트 활성 (CEO/CTO/Backend/CMO/FE/Legal Counsel). 도구 풀 비대.
- 각 에이전트 `mcp__claude-in-chrome__*` 호출처 grep → 실 사용 0 또는 미미한 에이전트 disable.
- 후보: Backend, CTO (사실상 미사용 per audit).

## 검증
- D: GET /api/companies/{id} → budgetMonthlyCents > 0 + alert 룰 active.
- H: 5 AGENTS.md grep 'HARD RULE' 0 hit (스킬로 이동), packlinx-governance skill 존재.
- I: Paperclip platform PR 또는 board ack.
-
