---
name: "[reminder] PACAA-1006 GSC '포장' 임프레션 +8주 측정 (2026-07-19)"
assignee: "ceo"
recurring: true
---

## 목적

PACAA-1006 kill criterion 측정. PACAA-1005 (포장 lead 카피 교체) deploy 완료 2026-05-24 → +8주 = 2026-07-19.

## 작업 (이 reminder 이슈에서 실행)

1. GSC (Search Console) https://search.google.com/search-console — 보드 Google 계정 로그인 의무.
2. Property = packlinx.com.
3. **Baseline 기간**: 2026-05-10 ~ 2026-05-24 (deploy -2w ~ deploy).
4. **Comparison 기간**: 2026-07-05 ~ 2026-07-19 (+6w ~ +8w).
5. 쿼리 필터: '포장 업체', '포장재 업체', '포장 회사', '포장업체', '포장재업체' (정확 일치 + contains '포장'). 
6. 두 기간 임프레션 합산 비교.
7. PACAA-1006 에 비교 표 코멘트 + 결정:
   - **≥+20%**: PACAA-1006 done, PACAA-1002 결정 검증 기록
   - **<+20%**: 보드 surface (request_confirmation 옵션 A 롤백 검토)
8. 본 reminder 이슈는 측정 완료 후 done.

## 출처
- 부모: PACAA-1006
- kill criterion 로그: $AGENT_HOME/runs/2026-05-24-1058-decisions.md
