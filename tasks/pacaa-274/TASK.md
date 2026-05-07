---
name: "GSC 수동 색인 요청 — 미색인 가이드 3건"
assignee: "cmo"
---

## 배경

[PACAA-269](/PACAA/issues/PACAA-269) 감사 결과: 200 응답하지만 Google에 미색인된 가이드 3건 발견.

## 대상

| URL | 상태 |
|---|---|
| /guides/plastic-container-guide | 200, 미색인 |
| /guides/packaging-printing-guide | 200, 미색인 |
| /guides/glass-metal-container-guide | 200, 미색인 |

## 작업

GSC URL Inspection 도구에서 각 URL 수동 색인 요청:
1. search.google.com/search-console → URL 검사
2. 각 URL 입력 → "색인 요청" 클릭

## Acceptance
- [ ] 3개 URL 색인 요청 완료 (GSC 제출 확인)
- [ ] 2주 후 색인 여부 확인 (soak window)
