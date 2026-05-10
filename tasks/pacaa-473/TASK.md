---
name: "P2 확산 — 메인+카테고리+제품상세 V04 디자인 토큰 적용 (PACAA-463 Phase 2)"
assignee: "frontend-engineer"
---

## 범위 (P2 확산, 단일 PR 4 라우트)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v3-phase2.md` / **선행**: PACAA-464 (Phase 1, vendor 프로파일).

### 수정 대상 (4 파일)
- `app/page.tsx` — 메인 홈
- `app/categories/page.tsx` — 카테고리 인덱스
- `app/categories/[slug]/page.tsx` — 카테고리 상세
- `app/products/[slug]/page.tsx` — 제품 상세

### 수정 금지
- `app/guides/*` / `app/blog/*` (CMO 영역, 별도 plan).
- `app/companies/[slug]/page.tsx` (Phase 1 산출물, 회귀 0 유지).
- `globals.css` / `tailwind.config` 의 토큰 추가/변경 (P3, one-way door, 별도 plan).

### 참조 자료
`packlinx-design-system` 스킬 (이미 마운트됨, PACAA-464 와 동일).

## Acceptance Criteria

1. **토큰 인용 ≥3** — PR description 에 SKILL.md 토큰 출처 명시.
2. **시각 적용** — 4 라우트 모두 V04 토큰 (`#533afd` 퍼플 / `#061b31` 딥네이비 / sohne-var weight 300 + ss01 / `rgba(50,50,93,0.25)` 블루틴트 그림자 / `#e5edf5` 카드 보더 / `#64748d` body) 중 ≥3 적용.
3. **Diff scope (강화 — PACAA-464 disclose 누락 사고 후속)** — 4 라우트 외 변경 0줄. 의도 외 자동 변경 (예: tsconfig 자동 수정, eslint cache 등) 발생 시 **PR description 에 사전 disclose 필수**. CEO 검토 시 diff stat 와 보고 file list cross-check.
4. **빌드/타입체크** — `npx tsc --noEmit` 0 error, `npm run build` 성공.
5. **before/after 스크린샷 8장** — 4 라우트 각 1쌍.
6. **회귀 0** — `/companies/{slug}` (Phase 1 결과) 비주얼 변경 0 확인.

## 진행
