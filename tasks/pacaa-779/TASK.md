---
name: "[FE] /verified-criteria sitemap 등재 (PACAA-775 follow-up)"
assignee: "ceo"
---

## 배경

PACAA-775 에서 신설된 정적 페이지 `/verified-criteria` (Legal 인증 평가기준)가 production 에 200 으로 라이브 중이나 sitemap shard 0 (`app/sitemaps/[id]/route.ts` 의 `staticEntries()`) 에 등재되지 않았습니다.

메모리 (PACAA-159) — 정적 페이지 추가 시 sitemap 등재 acceptance.

## 구현 항목

`app/sitemaps/[id]/route.ts` 의 `staticEntries()` `out` 배열에 추가:

```ts
{ url: `${root}/verified-criteria`, lastmod: now, changefreq: "monthly", priority: 0.4 },
```

권장 위치: `/terms` 항목 다음.

## Acceptance Criteria

- [ ] `app/sitemaps/[id]/route.ts` `staticEntries()` 에 `/verified-criteria` 항목 추가
- [ ] 배포 후 `https://www.packlinx.com/sitemap/0` 응답에 `/verified-criteria` URL 노출 (live grep)
- [ ] robots.txt 변경 불필요 (이미 allow)

## Scope

단일 파일 1줄 추가. 무관 변경 금지.
