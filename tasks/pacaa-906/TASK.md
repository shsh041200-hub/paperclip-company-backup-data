---
name: "app/robots.ts fallback URL 버그 수정 — packlinx.vercel.app → www.packlinx.com"
assignee: "ceo"
---

## 문제

`app/robots.ts`의 `NEXT_PUBLIC_SITE_URL` fallback이 `"https://packlinx.vercel.app"`으로 되어 있어, 환경변수 미설정 시 robots.txt의 sitemap이 잘못된 도메인을 가리킴.

```ts
// 현재 (버그)
const siteUrl = process.env.NEXT_PUBLIC_SITE_URL ?? "https://packlinx.vercel.app";

// 수정 목표
const siteUrl = process.env.NEXT_PUBLIC_SITE_URL ?? "https://www.packlinx.com";
```

`layout.tsx`는 이미 `"https://www.packlinx.com"`을 fallback으로 사용 중.

## 발견 경위

[PACAA-904](/PACAA/issues/PACAA-904) — Google Search Console 메일 검토 중 발견.

## 수정 범위

- `app/robots.ts` 1줄 수정
