---
name: "[감사 보고] 외부 감사자 시스템 보안·토큰 효율 점검 — 검토 후 보드 보고 요청"
assignee: "ceo"
---

## 📋 CEO 지시사항 (먼저 읽을 것)

이 이슈는 보드(창업자)가 외부 브라우저 자동화 에이전트(Claude in Chrome)에게 직접 의뢰한 시스템 감사 결과다. 다음 규칙을 엄수한다:

1. 자체 실행 금지: 본문 권장 조치(키 로테이션, intervalSec 변경, dangerouslySkipPermissions 해제 등)를 CEO 권한으로 직접 실행하지 말 것. 모두 보드 명시 승인 필요.
2. 2\. 검토만 수행: 출처·방법·결론의 타당성을 검증하고, 항목별로 동의/이견/추가확인 라벨링.
3. 3\. 보드 보고: 검토 완료 후 POST /api/issues/{this}/interactions kind\=request\_confirmation 으로 보드 결재 요청. 권장 조치 각 항목을 accept/reject 가능하게 구조화.
4. 4\. 하위 에이전트 공유는 보드 승인 후 CEO 명의로만 — PACAA-828 단일 채널 원칙 유지.

\---

## 🔍 감사 출처 및 방법

### 감사자

외부 브라우저 자동화 에이전트 (Claude in Chrome, 보드 로컬 세션). Paperclip 내부 에이전트 아님 — 보드 권한으로 UI + 내부 REST API 접근.

### 수행 경로 (시간 순)

Step 1 — UI 페이지 탐색

* /PACAA/dashboard, /PACAA/org, /PACAA/goals, /PACAA/costs
* \- /PACAA/agents/{ceo,backend-engineer,cto,cmo,frontend-engineer,legal-counsel,e5-worker,email-worker}/instructions
* \- /PACAA/agents/ceo/{skills,budget,runs,configuration}

Step 2 — 내부 API 호출 (DevTools fetch)

* GET /api/companies → packlinx\_company id\=d5e183da-c58f-4124-8075-493330dce4c4, status\=active, budgetMonthlyCents\=0, spentMonthlyCents\=608, requireBoardApprovalForNewAgents\=true, issueCounter\=919
* \- GET /api/companies/{id}/agents → 8개 에이전트 heartbeat 설정 일괄 수집
* \-
