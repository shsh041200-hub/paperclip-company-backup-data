---
name: "PACAA-490 FE r3 implement — 10 variant routes + 인덱스 비교 페이지 (보드 픽 surface 준비)"
assignee: "ceo"
---

## Context

CMO r3 brief 완료 (PACAA-495). 10 컨셉 axes·라우트명·FE 난이도 명세서: `plans/PACAA-490-r3-brief.md` (FE 작업 시작 전 정독). 보드 directive: 10개 만들어서 Chrome surface → 보드 1개 픽 → 9개 + 잔여 cleanup (PACAA-493 c7899cf9).

## 작업 범위 (preview only, 단일 PR)

### 1. 10 variant 라우트 (필수)

각 라우트 = `app/design-preview/main-r3-v01` ~ `main-r3-v10`. 각 폴더에:

- `page.tsx` (server component, `export const metadata` noindex/nofollow)
- `Main<RouteName>Client.tsx` (`'use client'`, 본 UI 로직)

CMO brief Part 2 의 10 컨셉 명세 (V01~V10) 그대로 implement. axes 매핑·CTA 위치·차별점 명시 준수. 라우트별 hero·1차 IA·2차 IA·CTA 충실 구현.

### 2. 인덱스 비교 페이지 (필수)

`app/design-preview/main-r3/page.tsx` (server component, noindex):
- 10 라우트 카드 그리드 (3×4 또는 2×5)
- 카드 = 컨셉명 (예 "V01 검색 게이트웨이") + 1줄 차별점 + 라우트 링크 + (선택) iframe thumbnail (`<iframe>` 미니 미리보기, lazy load, no-pointer-events overlay)
- 헤더: "r3 메인페이지 10 variant 비교" + 보드 안내 1줄 ("각 카드 클릭하여 라이브 보기 → 1개 선택")

### 3. Lock 유지 (전 라우트 공통)

- production `app/page.tsx`, `app/layout.tsx` 변경 0
- 다른 design-preview 라우트 변경 0 (v1/v2/v3 폴더는 PR scope 외; r3 cleanup 단계에서 별도 처리)
- 색: monochrome stripe-purple + neutral. amber/blue/green/red/yellow 0. V09 다크 hero 의 다크 배경은 purple-950 또는 neutral-950 만 OK
- 별점·인증 badge·Animated
