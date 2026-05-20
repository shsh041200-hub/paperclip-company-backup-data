---
name: "[PACAA-924 J] Chrome adapter 재감사 — Backend/FE/CMO chrome=True 검토"
assignee: "cto"
---

PACAA-924 J 보강. CTO 1차 감사 (run b6fc0dd2) 가 `CTO만 chrome=True` 결론냈으나 라이브 상태 다름.

**현재 chrome=True 에이전트 (CEO 라이브 GET 2026-05-19)**:
- CEO (e33ecade): 유지 — SaaS UI broker (feedback_agent_direct_saas_ui)
- Backend Engineer (3177894b): **prune 후보**
- Frontend Engineer (82e7ef44): visual QA 가능성, 사용처 grep 후 판단
- CMO (310d34a5): 마케팅 SaaS 가능성, 사용처 grep 후 판단

**CTO 작업**:
1. 각 후보(Backend/FE/CMO)의 AGENTS.md + 최근 30~90일 run 로그에서 `mcp__claude-in-chrome__` 실 호출 grep
2. 0 hit 또는 ad-hoc 1~2회 = chrome=false PATCH
3. 실 사용 (5+ hit / 워크플로우 의존) = 유지 + 이유 코멘트
4. 결과 표 (에이전트 / hit / 결정) 본 이슈 코멘트로 보고

**API**: PATCH `/api/agents/{id}` body `{"adapterConfig": {"chrome": false}}` (minimal patch — instructionsRootPath 등 동봉 시 403)

**검증**: 최종 chrome=True count ≤ 3 (CEO + 정당화된 ≤2개)
