---
name: "PACAA-548 production swap — companies-v1 → /companies/[slug] ship"
assignee: "frontend-engineer"
---

## 목표

보드 confirm 완료 (`f78fec66` accepted 2026-05-11T08:33:45Z). companies-v1 preview 디자인을 production `/companies/[slug]` 페이지에 swap ship.

## 작업

1. `app/design-preview/companies-v1/[slug]/page.tsx` 내용을 `app/companies/[slug]/page.tsx` 로 이식
2. `noindex` meta 제거 (production 페이지는 인덱싱 필요)
3. `revalidate` 설정 유지 (ISR 기존 값)
4. 새 브랜치 `feat/PACAA-548-companies-production-swap` 생성
5. PR 생성 (base: main)
6. `tsc --noEmit` 통과 확인

## Lock

- PR 생성 후 CEO 머지 (FE 직접 머지 금지)
- `app/design-preview/companies-v1/` 디렉토리는 별도 cleanup PR 또는 이번 PR 에 함께 삭제 OK
- 기존 PR #68 (preview-only) 은 자동 close 또는 swap PR 머지 후 cleanup

## Acceptance

- [ ] `/companies/{slug}` 라이브 200 + companies-v1 디자인 markers (hero 우상단 CTA, brand-50 stats row, 관련 가이드 3개, 모바일 sticky 하단 CTA, breadcrumb chevron)
- [ ] 대표 vendor 3개 (케이알포장재 / 명일씨앤비 / 대흥수출포장) 라이브 verify
- [ ] noindex 메타 부재 확인
- [ ] tsc --noEmit clean

## Reversibility

One-way (production swap). 단 P2 PACAA-551 와 동일 lean cycle, P2 시 검증 패턴 적용.

## 참고

- 부모: PACAA-548 (preview)
- P2 사례: PACAA-551 (categories swap, PR #67 commit `2404751`).
- Lean cycle 평균 사이클: audit 30분 + preview 10분 + 보드 accept 60-90분 + swap 머지 10분 + verify 5분.
