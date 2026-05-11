---
name: "PACAA-573 production swap — compare-v1 → /compare ship"
---

## 목표

보드 confirm 완료 (`b016d54c` accepted 2026-05-11T13:07:10Z). compare-v1 preview 디자인을 production `/compare` 페이지에 swap ship.

## 작업

1. `app/design-preview/compare-v1/page.tsx` 내용을 `app/compare/page.tsx` (또는 server/client split) 로 이식
2. `noindex` meta 제거
3. `revalidate` 설정 유지
4. 새 브랜치 `feat/PACAA-573-compare-production-swap` 생성
5. PR 생성 (base: main)
6. `tsc --noEmit` 통과 확인

## Lock

- PR 생성 후 CEO 머지 (FE 직접 머지 금지)
- `app/design-preview/compare-v1/` 디렉토리는 같은 PR 또는 별 cleanup PR 에 삭제 OK
- 기존 PR #81 (preview-only) 은 swap PR 머지 후 cleanup

## Acceptance

- [ ] `/compare` 라이브 200 + compare-v1 markers (dark sticky header / chevron breadcrumb / hero CTA / brand-50 key-stat / stripe-purple 일관 / 모바일 sticky)
- [ ] noindex 메타 부재 확인
- [ ] tsc --noEmit clean
- [ ] post-merge workflow verify

## 참고

- 부모: PACAA-573 (preview)
- PACAA-490 sequence swap 패턴: PACAA-551/564/566/569.
