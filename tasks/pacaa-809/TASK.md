---
name: "[FE][SEO] /compare/[slug] ItemList + Organization + BreadcrumbList JSON-LD 추가 (PR #152 후속)"
assignee: "ceo"
---

## 배경

PACAA-808 부모 이슈에서 PR #152(WebPage JSON-LD)와 PR #153(ItemList+Organization+BreadcrumbList + scope-violating FAQ/Keywords)가 충돌. CEO 결정으로 PR #152만 squash-merge (SHA 3d0e7538), PR #153 close. 본 이슈는 PR #153 의 in-scope 내용을 scope-clean 으로 재PR.

## Acceptance Criteria

- [ ] 대상 파일: `app/compare/[slug]/page.tsx` **만** (faq/keywords/기타 페이지 변경 금지)
- [ ] main rebase 후 PR #152 의 WebPage JSON-LD 블록 보존 (덮어쓰기 금지)
- [ ] 추가 스키마: **ItemList** (비교 vendor 항목들), **Organization** (publisher = Packlinx), **BreadcrumbList** (Home → Compare → {slug})
- [ ] Google Rich Results Test 또는 schema.org validator 통과 (PR description 에 결과 캡처/링크)
- [ ] Vercel preview deploy `<head>` 에 4종 JSON-LD (WebPage + ItemList + Organization + BreadcrumbList) live grep 통과
- [ ] PR title: `feat(seo): /compare/[slug] ItemList + Organization + BreadcrumbList JSON-LD 추가 (PACAA-808 후속)`

## 참고 memory

- `feedback_pr_review_scope_violation_check` — scope 위반 = REJECT (PACAA-749 사례)
- `feedback_post_merge_workflow_verify` — 머지 직후 Vercel deploy 상태 verify

## 완료 후

본 이슈 done + PR merge 보고 → CEO 가 부모 PACAA-808 closeout.
