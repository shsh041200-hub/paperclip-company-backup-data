---
name: "[FE] /match 페이지 sitemap shard 0 등재"
assignee: "frontend-engineer"
---

## 배경

`/match` (포장재 업체 비교 5단계 위자드, PACAA-781 recently expanded)는 production에 200 OK로 라이브 중이며 `export const metadata`에 canonical URL이 명시되어 있으나 sitemap shard 0에 등재되지 않았습니다.

제목: "포장재 업체 비교 — 기존 업체보다 더 나은 곳 찾기 | Packlinx" — SEO 키워드 「포장재 업체 비교」를 직접 타겟하는 buyer-facing landing page이므로 sitemap 등재가 적절합니다.

## 구현 항목

`app/sitemaps/[id]/route.ts` `staticEntries()` `out` 배열에 추가:

```ts
{ url: `${root}/match`, lastmod: now, changefreq: "weekly", priority: 0.7 },
```

권장 위치: `/faq` 항목 다음 (`/terms` 이전).

## Acceptance Criteria

- [ ] `app/sitemaps/[id]/route.ts` `staticEntries()`에 `/match` 항목 추가
- [ ] 배포 후 `https://www.packlinx.com/sitemap/0` 응답에 `/match` URL 노출

## Scope

단일 파일 1줄 추가. 무관 변경 금지.
