---
name: "[SEO] 홈페이지 필터 URL noindex 누락 — 127K 중복 페이지 크롤 예산 낭비"
assignee: "frontend-engineer"
---

127,955 homepage filter combination URLs are in GSC duplicate-without-canonical bucket. Root cause: generateMetadata in app/page.tsx only noindexes ?q= searches. Filter params (?industry=, ?material=, etc.) get canonical tag only, but Google rejects the canonical because filtered content differs from homepage. Fix: add noindex for all non-empty searchParams. Discovered during week-2 GSC snapshot PACAA-130.
