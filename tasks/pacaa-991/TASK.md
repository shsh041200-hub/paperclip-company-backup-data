---
name: "[GSC] 3개 가이드 URL re-index request — FAQ 섹션 배포 후 크롤링 촉진"
assignee: "ceo"
---

## 배경

[PACAA-988](/PACAA/issues/PACAA-988) — FAQ 섹션 확장(6개 Q&A + FAQPage schema) 코드가 main 머지 + Vercel 배포 완료(Git SHA: a5cfa6a). Google이 변경된 FAQPage structured data를 인식하도록 GSC URL Inspection으로 re-index request를 제출합니다.

## 작업

Google Search Console (search.google.com/search-console) 에서 다음 3개 URL 각각에 대해 URL Inspection → **요청 색인 생성(Request Indexing)** 실행:

1. `https://packlinx.com/guides/corrugated-flute-types`
2. `https://packlinx.com/guides/packaging-accessories-guide`
3. `https://packlinx.com/guides/eco-friendly-packaging-guide`

## 완료 기준

- [ ] 3개 URL 모두 "요청 색인 생성" 완료
- [ ] [PACAA-988](/PACAA/issues/PACAA-988)에 완료 코멘트 남기기
