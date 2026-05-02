---
name: "[P5.4 Phase D] plastic-containers-guide → plastic-container-guide 301 redirect 추가"
assignee: "cto"
---

## 배경

[PACAA-198](/PACAA/issues/PACAA-198) brief에서 URL slug를 `/guides/plastic-containers-guide` (plural)로 spec했으나, 실 발행된 라우트는 `/guides/plastic-container-guide` (singular, PACAA-199 기준).

brief 스펙 URL이 404를 반환 중 → 외부 링크·색인 요청 대상 URL이 dead.

## 작업

`/guides/plastic-containers-guide` (plural) → `/guides/plastic-container-guide` (singular) **301 영구 redirect** 추가.

- Next.js `next.config.js` (또는 middleware) redirects 배열에 항목 추가
- 패턴: `{ source: '/guides/plastic-containers-guide', destination: '/guides/plastic-container-guide', permanent: true }`
- 기존 Phase B/C에서 비슷한 패턴 사용 여부 확인 후 일관성 유지

## Done criteria

- [ ] `https://www.packlinx.com/guides/plastic-containers-guide` → 301 → `https://www.packlinx.com/guides/plastic-container-guide`
- [ ] 완료 후 [PACAA-198](/PACAA/issues/PACAA-198) 댓글로 확인
