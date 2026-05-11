---
name: "PACAA-549 production swap — guides-v1 → /guides + /guides/[slug] ship"
assignee: "frontend-engineer"
---

## 목표

보드 confirm 완료 (`3ae2d1bc` accepted 2026-05-11T09:15:21Z). guides-v1 preview 디자인을 production `/guides` (hub) 와 `/guides/[slug]` (detail) 페이지에 swap ship.

## 작업

1. `app/design-preview/guides-hub-v1/page.tsx` 내용을 `app/guides/page.tsx` 로 이식
2. `app/design-preview/guides-detail-v1/page.tsx` 내용을 `app/guides/[slug]/page.tsx` 로 이식 (각 guide 페이지가 단일 dynamic route 라면 component 이식)
3. `noindex` meta 제거 (production 페이지는 인덱싱 필요)
4. `revalidate` 설정 유지
5. 새 브랜치 `feat/PACAA-549-guides-production-swap` 생성
6. PR 생성 (base: main)
7. `tsc --noEmit` 통과 확인

## Lock

- PR 생성 후 CEO 머지 (FE 직접 머지 금지)
- `app/design-preview/guides-hub-v1/` + `app/design-preview/guides-detail-v1/` 디렉토리는 별도 cleanup PR 또는 이번 PR 에 함께 삭제 OK
- 기존 PR #75 (preview-only) 은 자동 close 또는 swap PR 머지 후 cleanup

## Acceptance

- [ ] `/guides` (hub) 라이브 200 + guides-v1 markers (시각 위계 정정, V05 token bridge, CTA fold-above 등)
- [ ] 대표 guide 3개 (`label-printing-guide`, `flexible-packaging-guide`, `cosmetic-packaging-box`) `/guides/{slug}` 라이브 verify
- [ ] noindex 메타 부재 확인
- [ ] tsc --noEmit clean
- [ ] post-merge workflow verify

## 참고

- 부모: PACAA-549 (preview)
- P2/P3 사례: PACAA-551 PR #67, PACAA-564 PR #73.
