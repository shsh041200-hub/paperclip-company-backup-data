---
name: "[SEO P1 → CTO] sitemap/1 (vendor 1380 URLs) 고아 — robots.txt 또는 sitemapindex 미참조"
assignee: "cto"
---

## 진단

라이브 probe (2026-05-11T07:45Z):

| 엔드포인트 | 형식 | URL 수 | 내용 |
| --- | --- | --- | --- |
| `/sitemap.xml` | urlset | 82 | 키워드 50 + 가이드 21 + 카테고리 6 + blog 2 + terms 1 + faq 1 |
| `/sitemap/0` | urlset | 231 | 가이드 21 + products 10 + categories 5 + services 1 |
| `/sitemap/1` | urlset | **1380** | **`/companies/{slug}` vendor 프로필 전부** |
| `/sitemap_index.xml` | 404 | — | sitemap index 엔드포인트 없음 |

`robots.txt`:
```
Sitemap: https://www.packlinx.com/sitemap.xml
Sitemap: https://www.packlinx.com/sitemap/0
```

**문제:** `/sitemap/1` 이 어디서도 참조되지 않음. robots.txt 에 없고, `/sitemap.xml` 도 urlset (sitemapindex 아님) 이라 chain 도 없음. Google Search Console 이 `/sitemap.xml` + `/sitemap/0` = 313 URLs 만 가시. **1380 vendor 프로필 URL 이 sitemap 으로 advertise 안 됨** (내부 링킹으로는 crawl 가능하지만 priority/lastmod 시그널 없음).

## 영향

- Vendor 프로필 = packlinx 핵심 검색 landing (구매자가 vendor 이름/특성으로 검색 → 프로필 진입). 1380 페이지 ≈ 사이트 inventory 의 80%+.
- SEO 1st priority (`Search engine + external visibility`, SOUL Phase 1.4) 직접 충돌.
- PACAA-117 (sitemap-index 분할), PACAA-395 (robots.txt sitemap/0 누락) 이전에 다룬 패턴의 후속 회귀. 1000-cap 해제 시 sharding 추가됐지만 advertise 메커니즘 분실.

## 가능 해결책 (CTO 선택)

**A. 최소 변경 — robots.txt 에 sitemap/1 추가:**
```
Sitemap:
