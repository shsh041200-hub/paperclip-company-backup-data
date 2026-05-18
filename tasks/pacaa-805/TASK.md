---
name: "[FE][SEO] /blog 2개 siteUrl 폴백 오류 — packlinx.com (no www) → canonical URL 불일치"
assignee: "ceo"
---

app/blog/2026-korea-packaging-trends/page.tsx 와 app/blog/packaging-rfq-guide/page.tsx 모두:
- siteUrl = process.env.NEXT_PUBLIC_SITE_URL ?? "https://packlinx.com" (no www)
- PR #143에서 다른 8개 파일 수정했지만 blog 2개는 누락

## 수정 범위
- 두 파일의 siteUrl 폴백을 "https://www.packlinx.com"으로 변경
- Article JSON-LD에 image 필드 추가 (${siteUrl}/og-default.png)

## PR #141/#146 관계
- PR #141: blog title 이중 브랜딩 수정 (이 이슈와 별도)
- PR #146: blog title:{ absolute } 수정 — siteUrl 폴백은 미포함
