---
name: "[SEO] /compare/* 내부링크 추가 — similarCompanies 섹션에 비교 링크 삽입 (PACAA-1027 후속)"
assignee: "frontend-engineer"
---

## 배경

PACAA-1027 CTO 분석: /compare/* 2주 미색인 주요 원인은 내부링크 완전 부재. 사이트맵에는 존재하나 어느 페이지에서도 정적 HTML 링크로 참조되지 않음.

## 작업

### /companies/[slug]/page.tsx — similarCompanies 섹션에 compare 링크 추가

이미 get_similar_companies RPC로 유사업체 fetch 중. 해당 섹션에 상위 2-3개 compare 정적 링크 추가.

비교 URL 형식: /compare/{alpha-sorted-slugA}-vs-{slugB}

/compare/-vs-

### 완료 기준

- /companies/[slug] 페이지 HTML에 정적 /compare/* href 존재 (curl로 확인)
- 기존 similar companies 섹션 UX 손상 없음
- git push origin main (정상 Vercel 빌드 확인)
