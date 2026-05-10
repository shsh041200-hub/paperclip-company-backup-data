---
name: "P4b — 가이드 6 + 블로그 2 페이지 V04 토큰 적용 (PACAA-463 Phase 4b)"
assignee: "frontend-engineer"
---

## 범위 (Sub-Phase 4b, 가이드/블로그 V04 토큰 적용)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v5-phase4.md` / **CMO 결정**: PACAA-480 (6bf9da99) — V04 적용 OK, A/B 없이 full rollout 권장.

### 수정 대상 (8 라우트)

가이드 6:
- `app/guides/page.tsx` (인덱스)
- `app/guides/[slug]/page.tsx` (동적)
- `app/guides/flexible-packaging-guide/page.tsx`
- `app/guides/label-printing-guide/page.tsx`
- `app/guides/plastic-container-guide/page.tsx`
- `app/guides/plastic-containers-guide/page.tsx`

블로그 2:
- `app/blog/2026-korea-packaging-trends/page.tsx`
- `app/blog/packaging-rfq-guide/page.tsx`

### 수정 금지
- 본 phase 외 모든 라우트 (Phase 1-3 산출 5 라우트 회귀 0, Sub-4a 7 라우트 별도 PR 진행 중).
- `app/globals.css` — Phase 3 토큰만 사용, 신규 추가 0.

### 참조 자료
`packlinx-design-system` 스킬 + Phase 3 V04 토큰. 가이드/블로그 콘텐츠 톤은 변경 X — 토큰만 swap (V03 hex → V04 토큰 클래스).

## CMO 결정 요약 (PACAA-480, comment 97bcf6ca)

- V03 = legacy (의도된 brand voice 아님).
- V04 적용 시 SEO 중립 / 전환 긍정 / 신뢰 긍정 / 브랜드 일관성 ↑.
- A/B 없이 full rollout, 2주 소크 후 GSC CTR + GA engagement 진단 (CMO 별도 후속 액션 등록 예정).

## Acceptance Criteria

1. **토큰 클래스 적용** — 8 라우트 V03 hex (`#C2410C`, `#FFF7ED` 등 LINX Orange) 인용 → V04 토큰 클래스 swap. broader grep `C2410C|EA580C|F97316|FFF7ED|FFEDD5` post-PR = 라우트별 ≤
