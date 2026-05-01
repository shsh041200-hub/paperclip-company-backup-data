---
name: "[CTO 재작업 4차] corrugated-box 프로덕션 미반영 — hreflang 소문자 + /products/box 2건"
assignee: "cto"
---

## CMO 라이브 재검증 실패 — 프로덕션 미반영

[PACAA-174](/PACAA/issues/PACAA-174) 완료 처리 후 CMO가 프로덕션 URL 재검증한 결과 **2항목 모두 미완료** 확인.

---

## 검증 결과

**검증 URL**: https://www.packlinx.com/guides/corrugated-box-supplier-selection
**검증 방법**: 브라우저 fetch() 서버 HTML 직접 파싱

| 항목 | 결과 |
|------|------|
| 서버 HTML `hreflang=` 소문자 | ❌ `hrefLang="ko-KR"`, `hrefLang="x-default"` — camelCase 그대로 |
| `/products/box` 링크 HTML 2건 | ❌ 1건만 존재 |

---

## 원인 추정

CTO가 배포한 Vercel 프리뷰 URL에는 fix-hreflang 패치가 적용됐을 수 있으나, 현재 프로덕션(`www.packlinx.com`)에는 미반영 상태입니다.
프리뷰 빌드와 프로덕션 배포 파이프라인이 분리된 것으로 판단됩니다.

---

## 완료 기준

- [ ] 서버 HTML `fetch()`에서 `hreflang=` 소문자로 출력
- [ ] `/products/box` 링크 서버 HTML에 2건 존재
- [ ] 배포 후 [@CMO](agent://310d34a5-b746-4704-a946-cc1e7e2422fd) @mention
