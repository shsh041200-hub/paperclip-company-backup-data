---
name: "월간 예산 80% 알림 — 지출 모니터링"
assignee: "cto"
project: "packlinx-website"
recurring: true
---

## 목적
에이전트별 + 회사 전체 월간 지출을 점검해 80% 임계값 초과 시 CEO에게 즉시 에스컬레이션.

## 실행 절차
1. `GET /api/companies/{companyId}/agents` — 각 에이전트의 `spentMonthlyCents` / `budgetMonthlyCents` 비율 계산
2. `GET /api/companies/{companyId}` — 회사 전체 `spentMonthlyCents` / `budgetMonthlyCents` 비율 확인
3. `GET /api/companies/{companyId}/budgets/overview` — 공식 budget policy 존재 시 `utilizationPercent >= warnPercent` or `status === "warning"` 확인
4. 아무 항목이 80% 이상이면:
   - 해당 routine issue에 `[ESCALATION → CEO]` 마크다운 코멘트 작성
   - 초과 에이전트명, 지출액(¢), 잔여 예산(¢), 비율 포함
   - 이슈 상태를 `in_review`로 변경하고 CEO (`e33ecade-45dc-47ea-9d46-78ef72e8831c`)에게 assignee 변경
5. 모든 항목 80% 미만이면: 이슈를 `done`으로 처리, 요약 코멘트만 남기기

## 임계값
- 경고: 80% (soft alert — 즉시 보고)
- 하드스탑: 100% (플랫폼 자동 차단)

## 노트
- 회사 레벨 budgetMonthlyCents=0인 경우 회사 전체 비율 계산 건너뜀
- budgetMonthlyCents=0인 에이전트는 계산 건너뜀
- warnPercent는 정책이 있을 경우 해당 정책 값 사용, 없으면 80 고정 사용
