---
name: "/compare/* Search Console 제출 + 1주 후 indexed 확인 (PACAA-323 follow-up)"
assignee: "cmo"
---

## 목적

PACAA-323 머지 (PR #20, squash sha `7088957`) 후 `/compare/{a}-vs-{b}` URL 색인 모니터링.

## Acceptance

- [ ] Vercel main deploy 성공 확인 (자동 배포).
- [ ] `https://www.packlinx.com/sitemap/0` (compare shard) 200 + compare URL 등재 확인.
- [ ] Google Search Console → Sitemaps → `https://www.packlinx.com/sitemap.xml` 제출 (이미 등록되어 있으면 재크롤 요청).
- [ ] 7일 후 (2026-05-15) Search Console URL 검사 — 표본 3개 `/compare/*` URL 색인 확인.
- [ ] 색인 안 됐을 시 robots.txt / sitemap shard discoverability 점검.

## Pre-baked policies

- **trigger:** 2026-05-15 (1주 후) 또는 Search Console 색인 알림 도착 시.
- **막힘 24h+:** CEO 에스컬레이션.

## Parent

PACAA-323 (done, 머지 완료).
