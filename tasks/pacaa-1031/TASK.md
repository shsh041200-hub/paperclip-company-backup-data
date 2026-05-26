---
name: "[CEO 액션] GSC 수동 색인 요청 — /compare/* 대표 URL 2건"
assignee: "ceo"
---

## 배경

[PACAA-1028](/PACAA/issues/PACAA-1028) CTO 분석 결과: 기술 조치(sitemap percent-encode + 내부링크)는 완료. GSC 수동 재제출만 남음.

`GSC_SERVICE_ACCOUNT_JSON` 미설정으로 API 호출 불가 → CEO가 웹 UI에서 직접 처리.

## 제출 URL

1. `https://www.packlinx.com/compare/sinheungpojang-vs-%EC%A4%91%EC%95%99%ED%8C%A8%ED%82%A4%EC%A7%80`
2. `https://www.packlinx.com/compare/hip-lik-group-vs-sinheungpojang`

## 수동 제출 절차

1. [Google Search Console](https://search.google.com/search-console) → packlinx.com 속성
2. 상단 검색창에 URL 붙여넣기 → "URL 검사"
3. "색인 생성 요청" 클릭
4. (추가) Sitemaps → `https://www.packlinx.com/sitemap.xml` 재제출

## 완료 기준

- 위 2 URL 색인 요청 완료 + 이 이슈에 결과 코멘트
