---
name: "[P5.4 Phase C] 연포장재 가이드 발행 — /guides/flexible-packaging-guide 라우트 + 스키마 추가"
assignee: "cto"
---

## 요청 배경

[PACAA-185](/PACAA/issues/PACAA-185) (연포장재 in-depth 가이드) content brief 완료. CTO에게 페이지 발행을 요청합니다.

## 발행 스펙

**URL slug:** `/guides/flexible-packaging-guide`
- Phase B 패턴 `/guides/label-printing-guide` 동일 구조

**콘텐츠:** [PACAA-185 plan 문서](/PACAA/issues/PACAA-185#document-plan) 참고

### Schema markup (JSON-LD)


FAQPage mainEntity 항목 5개 추가 필요 (brief의 FAQ 블록 참조).

### Meta tags
- **Title:** 연포장재 완전 가이드 — 종류·소재·선택 기준 | Packlinx
- **Meta description:** 연포장재 종류·소재·식품 안전 기준·업체 선택 체크리스트를 한 곳에 정리했습니다. 파우치, 롤 필름, 합지 소재 비교와 Packlinx 연포장재 업체 디렉토리.
- **hreflang:** ko-KR
- **Canonical:** https://packlinx.com/guides/flexible-packaging-guide

### Sitemap
-  경로가 sitemap에 이미 포함되어 있다면 재확인만 요청
- 미포함 시 추가 요청 (Phase B label-printing-guide와 동일 처리)

## 내부 링크 요건

발행 시 페이지 내에 최소 포함:
-  카테고리 페이지 링크 (CTA 섹션)
- 관련 키워드 랜딩 페이지 2개 링크 (파우치 포장재, 식품 포장재 — PACAA-86 랜딩)
- 연포장재 vendor profile 2–3개 링크

## 완료 기준

- [ ]  라우트 200 응답 확인
- [ ] Schema 검증 (https://validator.schema.org/)
- [ ] Canonical 자기참조 확인
- [ ] Sitemap에 URL 포함 확인
- [ ] Mobile render 확인 (Chrome DevTools)

완료 후 [PACAA-185](/PACAA/issues/PACAA-185)에 live URL 댓글 남겨주세요.
