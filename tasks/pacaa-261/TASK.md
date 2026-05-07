---
name: "GSC 5xx 서버 오류 3페이지 분석 (5/07 리포트 surface)"
assignee: "cto"
---

## 트리거

2026-05-07 GSC Coverage 리포트 (보드 이메일 도착, PACAA-129 첨부 분석 결과) — "서버 오류(5xx)" 카테고리에 **3 페이지** surface. baseline 4/27 / 5/01 리포트엔 없던 신규 신호.

## 작업

1. GSC > 색인 생성 > 페이지 > "서버 오류(5xx)" 클릭 → 영향 받은 3 URL 확보 (스크린샷 첨부)
2. 각 URL 라이브 probe (`curl -A Googlebot`) — 현재 200/308/5xx 어디 인지
3. 5xx 재현 시 root cause 파악:
   - Vercel 빌드 타임아웃?
   - Edge function cold-start timeout?
   - 특정 라우트 (`[slug]`) 의 데이터 fetch 실패?
   - 어떤 deployment 시점에 발생했는지 Vercel 로그 cross-check
4. 수정 또는 "transient, 영향 없음" 판정 기록
5. 수정 시 GSC 「수정 검증」 클릭

## 판정 기준

- 3 URL 모두 현재 200/308 정상 → transient. 결과 기록 후 done.
- 1+ URL 재현 가능 5xx → fix + GSC 검증 요청.
- 동일 패턴 신규 발생 시 PACAA-119 escalation.

## 컨텍스트

- 관련 이슈: PACAA-129 (1주차 4xx 측정), PACAA-119 (P1.D GSC validation)
- 라이브 사이트 광범위 probe 결과 (5/07 09:23 KST CEO 측):
  - `https://packlinx.com/` → 308 → www 200
  - `https://packlinx.com/sitemap.xml` → www/sitemap-index 200 (2 children)
  - `https://packlinx.com/robots.txt` → www 200
  - `https://keywords.packlinx.com/` → 200
  → 광범위 fire 아님, 3 URL 한정 transient 가능성 높음
- baseline raw 데이터: `plans/PACAA-113/2026-05-07/packlinx.com-Coverage-2026-05-07.xlsx`

## Acceptance

- [ ] GSC 5xx 카테고리 3 URL 식별 + 코멘트 기록
- [ ] 각 URL 라이브 probe 결과 기록
-
