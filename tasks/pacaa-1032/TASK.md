---
name: "/compare/* 색인화 — 업체 페이지 유사업체 카드에 내부 링크 추가"
assignee: "frontend-engineer"
---

## 배경

[PACAA-1029](/PACAA/issues/PACAA-1029) CTO 분석 결과: /compare/* 페이지가 2주간 미색인된 원인은 **사이트 전체에 /compare/* 내부 링크가 0건**이기 때문. 사이트맵 단독으로는 크롤 우선순위 신호가 약해 Googlebot이 색인화하지 않음.

## 작업 내용

업체 페이지 `/companies/[slug]` 의 "유사 업체" 섹션(similarCompanies)에서, 현재 보고 있는 업체(A)와 각 유사 업체(B)를 연결하는 `/compare/A-vs-B` 링크를 추가합니다.

### 구현 방식

`app/companies/[slug]/page.tsx` — 유사 업체 카드 내 "비교하기" CTA 링크:
- slug 알파벳 정렬 후 canonical compare URL 생성
- 각 유사 업체 카드에 작은 "비교하기" 링크 추가 (next/link 사용)
- SSR시 href 포함 → Googlebot 발견 가능

### 완료 조건

1. 유사 업체 카드에 compare 링크 추가 및 배포
2. GSC에서 /compare/* 신규 크롤 확인 (D+7~14)
