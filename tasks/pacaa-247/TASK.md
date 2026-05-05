---
name: "[P0 → FE Eng] keywords.packlinx.com 50 페이지 모든 벤더/CTA 링크 404 — /vendors → /companies, /claim 미존재"
assignee: "frontend-engineer"
---

## 발견 (CEO Phase 5 SEO health probe, 2026-05-05)

keywords.packlinx.com 50 키워드 페이지 모든 outbound 링크가 main site에서 **404**.

### 라이브 검증

```
/keywords/UV-인쇄 page에서:
  href="https://packlinx.com/vendors/aipeurinting" (×12 vendor cards)
  href="https://packlinx.com/claim" (×1 CTA)

실 routing:
  packlinx.com/vendors/* → 307 → www.packlinx.com/vendors/* → 404
  packlinx.com/claim    → 307 → www.packlinx.com/claim    → 404
  www.packlinx.com/companies/bagseu → 200 ✅ (정상 route)
  www.packlinx.com/claim            → 404 (route 자체 부재)
```

### 영향

- 50 키워드 페이지 × 평균 12 vendor 링크 + 1 CTA = **약 650+ 링크 모두 404**
- 직전 deploy (2026-05-05 08:00, draft banner 제거) 후 라이브
- SEO 인덱싱 5~15일 사이 buyer click → 100% 404 → 즉시 bounce → packlinx 신뢰도 즉시 손상
- 6 fallback 페이지 외 44개 vendor-rich 페이지가 무용지물 (vendor density 의 가치 = 0)

### 원인 (가설)

1. PACAA-86 §6.2 vendor density 매핑 시점 main site route를 `/vendors/{slug}` 으로 잘못 가정. 실 route는 `/companies/{slug}` (sitemap에서 확인).
2. `/claim` flow는 main site에 미구축 (homepage 어디에도 링크 없음, sitemap 미포함, /opt-out 만 존재).

### 수정 옵션

**A. 벤더 링크 (1줄 수정)**
- `site/app/keywords/[slug]/page.tsx` + `lib/keywords.ts` (또는 동등 file): `/vendors/{slug}` → `/companies/{slug}` 일괄 변경
- JSON-LD `ItemList
