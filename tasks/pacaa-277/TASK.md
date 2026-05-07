---
name: "[보드 directive] AGENTS.md 전사 propagation — sub-agent ↔ board 직접 통신 금지 + 즉시 escalation 의무"
assignee: "cto"
---

## 배경
PACAA-263 보드 directive 06e68a06 (2026-05-07) — 새 운영 모델:
1. **CEO 외 sub-agent 는 보드 응답 대기 금지.** 보드 입력 필요 항목은 CEO 에 escalate, CEO 가 텔레그램(interaction)으로 broker.
2. **sub-agent 는 CEO 액션·검토·승인 필요 시 즉시 escalation/호출.** in_review status PATCH 만 하고 sleep 금지 — 작업 일시 연체.

## 작업
모든 sub-agent (CTO, Backend Engineer, Frontend Engineer, CMO, Legal Counsel, E5 Worker) 의 AGENTS.md / 시스템 프롬프트 / 인덱스 메모리에 위 2 룰 박기.

구체적으로 다음 섹션 추가:
- **"보드 직접 통신 금지"** — ask_user_questions / request_confirmation 보드 대상 발의 금지. 보드 입력 필요 시 CEO 에 escalation 코멘트.
- **"즉시 escalation 의무"** — CEO 검토 / 승인 필요 시 in_review PATCH 와 동시에 명시적 "CEO 검토 요청: ___" escalation 코멘트. status PATCH 만 하고 sleep 금지.

## Acceptance
- [ ] CTO/Backend/Frontend/CMO/Legal AGENTS.md 모두 위 2 룰 추가 (PR 시리즈)
- [ ] 각 agent 인덱스 메모리에 reference 추가
- [ ] PR 머지 + 라이브 — 다음 sub-agent wake 부터 적용
- [ ] 메모리 baked: feedback_subagent_never_direct_to_board.md / feedback_subagent_immediate_escalation.md (CEO 측 — 이미 baked)

## Reversibility
AGENTS.md 수정 = reversible. 보드 directive 라 보드 승인 게이트 통과.

## 의존성
없음 — 즉시 시작.
