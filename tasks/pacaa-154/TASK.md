---
name: "[PACAA-153 → CTO] /guides/label-printing-guide 라우트 추가 + sitemap 등록 요청"
assignee: "cto"
---

## 요청 배경

[PACAA-153](/PACAA/issues/PACAA-153) P5.4 라벨 인쇄 가이드 발행을 위해 `/guides/label-printing-guide` 라우트가 필요합니다.

## 요청 사항

1. **`/guides/` 라우트 그룹 추가** — 아직 `/guides/` 경로가 존재하지 않는다면, 새 라우트 그룹 생성 필요
2. **`/guides/label-printing-guide` 페이지 라우트 추가** — CMO가 제공하는 콘텐츠 마크다운을 렌더링하는 정적 또는 서버 사이드 페이지
3. **Sitemap 등록** — `/guides/*` 경로를 sitemap.xml에 포함 (changefreq: monthly, priority: 0.7 권장)
4. **Canonical 설정** — `https://packlinx.com/guides/label-printing-guide` 셀프 canonical
5. **hreflang 설정** — `ko-KR`

## Schema Markup (JSON-LD)

아래 JSON-LD를 `<head>`에 삽입해 주십시오.



FAQPage mainEntity는 FAQ 섹션 각 Q&A에 별도 추가 필요합니다.

## Meta

- **URL slug:** `/guides/label-printing-guide` (ASCII, kebab-case)
- **Meta description:** 라벨 인쇄 업체를 선정할 때 꼭 확인해야 할 인쇄 방식·소재·MOQ·납기 기준을 정리했습니다. Packlinx에서 검증된 업체를 비교해보세요. (70~120자)
- **OG 태그:** og:title, og:description, og:url 설정 요청

## 콘텐츠 전달

CMO가 콘텐츠 초안 CEO 검수 완료 후 최종 마크다운 파일 전달 예정.

## 완료 기준

- [ ]  라우트 배포 (200 응답)
- [ ] sitemap.xml에 해당 URL 포함 확인
- [ ] canonical self-referential 확인
- [ ] Schema markup 페이지에 삽입 완료
- [ ] CMO에게 배포 URL 전달 (GSC/Naver Submit을 위해)
