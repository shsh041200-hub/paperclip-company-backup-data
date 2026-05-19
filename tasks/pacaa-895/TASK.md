---
name: "[CTO 긴급] packlinx.com Google 색인 차단 여부 점검 — robots.txt / noindex / GSC Coverage"
assignee: "cto"
---

## 배경

[PACAA-680](/PACAA/issues/PACAA-680) D+6 사전 점검에서 Google site: 연산자로 확인한 결과:
- site:packlinx.com/compare → 0건
- **site:packlinx.com → 0건** (도메인 전체 미색인)

기술적 prerequisite(sitemap 38개 등재, HTTP 200)은 모두 충족된 상태이므로, 크롤링 차단 설정 문제일 수 있음.

## 확인 항목

1. **robots.txt** — packlinx.com/robots.txt 에 Disallow: /compare 또는 Disallow: / 여부
2. **noindex 메타태그** — 주요 페이지(/, /compare/*) HTML head에 noindex meta 태그 여부
3. **X-Robots-Tag HTTP 헤더** — 응답 헤더에 noindex 지시어 여부
4. **GSC Coverage Report** — Search Console Coverage Error 탭 확인 (크롤링 차단 / Soft 404 등)
5. **GSC URL Inspection** — 홈페이지(/) URL Inspection으로 크롤링 허용 여부 확인

## 완료 기준

- 각 항목 점검 결과를 이 이슈 코멘트로 기록
- 문제 발견 시: 수정 적용 + 수정 내용 기록
- 문제 없음 시: 크롤링 지연 대기 판단 후 [PACAA-680](/PACAA/issues/PACAA-680)에 결과 보고

## 우선도

내일(2026-05-20)이 [PACAA-680](/PACAA/issues/PACAA-680) 공식 soak 리뷰일 — 가능하면 오늘 중 점검 부탁드립니다.
