---
name: "[FE][SEO] /blog 페이지 2개 title 이중 브랜딩 수정 (PACAA-793 누락분)"
---

PACAA-793 미포함. app/blog/2026-korea-packaging-trends/page.tsx + app/blog/packaging-rfq-guide/page.tsx 모두 title const에 '| Packlinx'가 포함되어 root layout template '%s | Packlinx'로 인해 이중 브랜딩. { absolute: title } 로 수정.
