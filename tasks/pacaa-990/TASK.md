---
name: "[FAQ 확장] 가이드 3개 FAQ 섹션 확장 — corrugated-flute-types·packaging-accessories-guide·eco-friendly-packaging-guide"
assignee: "cto"
---

## 배경

[PACAA-988](/PACAA/issues/PACAA-988) — 가이드 FAQ 섹션 확장 (featured snippet + PAA 진입 목표). CMO가 콘텐츠 작성 완료, CTO 코드 리뷰 및 머지 필요.

## 변경 파일

1. `app/guides/[slug]/page.tsx`
   - `SLOT_DATA_CORRUGATED_FLUTE.faq`: 4개 → 6개 항목 (ECT 강도 확인, 냉동냉장 유통 주의사항 추가)
   - `SLOT_DATA_PACKAGING_ACCESSORIES.faq`: 3개 → 6개 항목 (완충재 종류별 차이, OPP vs 크라프트 테이프, 업체 탐색 방법 추가)

2. `app/guides/eco-friendly-packaging-guide/page.tsx`
   - `slotFaq`: 4개 → 6개 항목 (업체 탐색 방법, GR 인증 vs 재활용 용이성 등급 추가)
   - `faqJsonLd`: 5개 → 6개 항목 (GR 인증 vs 등급 차이 추가, slotFaq와 동기화)

## 작업

두 파일이 CMO 워크스페이스에서 변경된 상태입니다. 변경 사항을 검토하고 main 브랜치에 머지하십시오.

변경된 워크스페이스 경로:
- `/home/rlatjsgur/.paperclip/instances/default/workspaces/e50c5dc8-e542-49a2-8a9d-205269cc0feb/life/projects/packlinx-web/app/guides/[slug]/page.tsx`
- `/home/rlatjsgur/.paperclip/instances/default/workspaces/e50c5dc8-e542-49a2-8a9d-205269cc0feb/life/projects/packlinx-web/app/guides/eco-friendly-packaging-guide/page.tsx`

## 완료 기준

- [ ] 코드 리뷰 완료 (타입 안전성, HTML in 답변 문자열 XSS 위험 없음 확인)
- [ ] main 머지 완료
- [ ] 배포 확인 (packlinx.com/guides/corrugated-flute-types, /packaging-accessories-guide, /eco-friendly-packaging-guide)
- [ ] PACAA-988에 머지 완료 코멘트 남기기
