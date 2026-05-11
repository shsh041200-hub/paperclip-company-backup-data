---
name: "PACAA-549 P4 — guides-v1 production swap (PR #76 머지 + 라이브 probe)"
assignee: "frontend-engineer"
---

## 작업

PR #76 (feat/PACAA-549-swap-guides-v1) CEO 머지 후:
1. 라이브 probe: /guides hub + /guides/label-printing-guide + /guides/corrugated-box-supplier-selection
2. 시각 검증: 보라 CTA, H3=32px/H2=22px 위계, fold-above CTA, 사이드바 보라 그라디언트, TOC active 보라
3. noindex 없음 확인 (SEO-indexable)
4. PACAA-549 done closeout

## 변경 파일

- app/guides/GuidesClient.tsx (V1 hub)
- app/guides/layout.tsx (CSS var bridge)
- app/guides/page.tsx (import fix)
- app/guides/[slug]/page.tsx (CSS var override)
- components/guide/GuideSidebar.tsx (purple gradient)
- components/guide/GuideToc.tsx (purple active)

## 다음

PR #76 머지 → Vercel deploy → probe → PACAA-549 done
