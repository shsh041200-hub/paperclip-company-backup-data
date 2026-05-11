---
name: "PACAA-550 production swap — faq-v1 → /faq ship"
assignee: "frontend-engineer"
---

## 목표

보드 confirm 완료 (`4e267667` accepted 2026-05-11T09:50:14Z). faq-v1 preview 디자인을 production `/faq` 페이지에 swap ship. **시퀀스 마지막 페이지.**

## 작업

1. `app/design-preview/faq-v1/page.tsx` 내용을 `app/faq/page.tsx` 로 이식 (카테고리 그룹화 + jump nav + 앵커 link + URL hash)
2. `noindex` meta 제거 (production 페이지는 인덱싱 필요)
3. `revalidate` 설정 유지
4. 새 브랜치 `feat/PACAA-550-faq-production-swap` 생성
5. PR 생성 (base: main)
6. `tsc --noEmit` 통과 확인

## Lock

- PR 생성 후 CEO 머지 (FE 직접 머지 금지)
- `app/design-preview/faq-v1/` 디렉토리는 별도 cleanup PR 또는 이번 PR 에 함께 삭제 OK
- 기존 PR #78 (preview-only) 은 swap PR 머지 후 cleanup

## Acceptance

- [ ] `/faq` 라이브 200 + faq-v1 markers (카테고리 그룹화, jump nav, 앵커 link, URL hash 동작)
- [ ] noindex 메타 부재 확인
- [ ] tsc --noEmit clean
- [ ] post-merge workflow verify

## 참고

- 부모: PACAA-550 (preview)
- P2/P3/P4 사례: PACAA-551 PR #67, PACAA-564 PR #73, PACAA-566/567 PR #76.
- **P5 done = PACAA-490 umbrella 100% closing**
