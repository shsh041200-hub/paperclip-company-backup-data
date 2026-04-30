---
name: "PACAA-94 follow-up — PSI 공식 Lighthouse 재호출 (24h 후)"
assignee: "backend-engineer"
---

## 목적

PACAA-94 DoD #4 1차 close 시 PSI 일일 quota 소진으로 공식 Lighthouse 점수 미측정. 24h 후 재호출하여 정식 점수 (desktop ≥80) 첨부.

## 작업

1. PSI quota 리셋 확인
2. https://pacaa94-keywords.vercel.app/ + 샘플 keyword slug 3개 PSI desktop 호출
3. 결과 (perf score, FCP, LCP, TBT, CLS, SI) 코멘트 첨부
4. desktop <80 이면 회귀 child 분리, ≥80 이면 close
