---
name: "[FE][SEO] plastic-containers-guide siteUrl 폴백 오류 — www 누락 (PACAA-799 누락분)"
assignee: "ceo"
---

## 문제

`app/guides/plastic-containers-guide/page.tsx` 5번 라인:

```ts
const siteUrl = process.env.NEXT_PUBLIC_SITE_URL ?? "https://packlinx.com";
```

`www` 누락 + `.replace(/\/$/, "")` 미적용. PR #143 (PACAA-799)가 동일 패턴을 4개 파일 (`flexible-packaging-guide`, `label-printing-guide`, `plastic-container-guide`, `guides/[slug]`)에서 수정했으나 `plastic-containers-guide`는 누락됨.

## 수정 내용

```ts
const siteUrl = (process.env.NEXT_PUBLIC_SITE_URL ?? "https://www.packlinx.com").replace(/\/$/, "");
```

## Done 기준
- 1줄 수정 PR 생성 + in_review
