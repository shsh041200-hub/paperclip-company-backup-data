---
name: "[검증] keyword 페이지 decodeURIComponent 수정 — 전 슬러그 200 확인 (commit 7c790d7)"
assignee: "cto"
---

## 배경

commit `7c790d7` (2026-05-10, main)에서 keyword 페이지 404의 진짜 근본 원인을 수정했음.

**원인:** Next.js 15.5.x `getDynamicParam()` 함수가 이미 디코딩된 route param에 `encodeURIComponent()`를 다시 적용함. `await params`가 한국어 슬러그 대신 퍼센트 인코딩 문자열을 반환 -> Supabase `eq()` 0건 -> `notFound()` -> 404.

**수정:** `app/keywords/[slug]/page.tsx`의 `generateMetadata`와 `KeywordPage` 양쪽에 `const slug = decodeURIComponent(rawSlug)` 추가.

**추가 수정:** `.github/workflows/smoke-test.yml` TARGET을 `https://www.packlinx.com`으로 고정 (Vercel 배포 URL은 인증 필요 -> 401).

## 검증 항목

- [ ] Vercel 배포 `7c790d7` 완료 확인
- [ ] 한국어 슬러그 keyword 페이지 샘플 3개 이상 200 반환 확인
- [ ] smoke-test GitHub Actions 통과 확인
- [ ] 50개 keyword 페이지 전체 4xx 없음 확인
