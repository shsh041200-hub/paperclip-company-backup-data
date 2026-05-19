---
name: "[CTO] API-level enforcement: POST /interactions = CEO-only (PACAA-828)"
assignee: "ceo"
---

## 배경

PACAA-828 보드 지시: 보드 텔레그램 발의 권한을 CEO 단독으로 제한. 모든 sub-agent 의 AGENTS.md / HEARTBEAT.md / SOUL.md / packlinx-comms SKILL 은 정책 hard rule 로 갱신 완료. 정책만으로는 "무결점" 보장이 안 됨 — 미래의 instruction drift / 신규 에이전트 hire 검수 누락 / LLM hallucinated curl 등 leak vector 가 남는다. 플랫폼 레벨 enforcement 가 필요.

## 요구사항

POST /api/issues/{issueId}/interactions 핸들러에서 요청 발신 agent 의 role 이 ceo 가 아니면 403 반환.

- 적용 범위: kind=request_confirmation / ask_user_questions / suggest_tasks (텔레그램 3종)
- 발신자 식별: 기존 Bearer JWT 의 agentId → agents.role lookup
- local-board (Bearer 없는 호출) 영향 없도록 유지
- 403 body: error code interactions_ceo_only + 메시지

## Acceptance

- [ ] CEO 토큰 POST interaction 200 (기존 동작 보존)
- [ ] CTO/CMO/BE/FE/Legal 토큰 POST interaction 403
- [ ] 회귀 테스트 1건 추가 (CEO 200 + sub-agent 403)
- [ ] PATCH /interactions/{id} 변종 있으면 동일 게이트
- [ ] role IS NULL 도 403 (안전 default)

## 노트

정책 patch 는 본 heartbeat 에 라이브. 본 platform patch 는 잔여 leak vector 0 을 위한 페어 fix.
