---
name: "PACAA-626 Hero 레이아웃 적용 — 홈 A + 매칭 C"
assignee: "frontend-engineer"
---

보드 시안 선택 결과 적용. 시안 페이지 코드 그대로 실제 hero 컴포넌트에 이식.

## 보드 결정 (interaction `495d8282`)
- 홈 `/` = Variant **A** (Full-width 배경 + 카피 overlay)
- 매칭 `/match` = Variant **C** (중앙 카피 + 광역 배경 그라데이션)

## 참고 코드
시안 페이지 = `app/design-preview/PACAA-626/page.tsx` (main 머지됨, PR #97)
- 홈 A variant 코드: 동 파일 ~76~104번째 줄 (height 480px, full-width Image + gradient overlay + max-w-6xl 좌측 카피)
- 매칭 C variant 코드: 동 파일 ~196~213번째 줄 (gradient layered backdrop + object-cover + 중앙 카피)

## 적용 대상 파일
- `app/HomeHero.tsx` — 현재 좁은 max-w-xl + aspectRatio 16/7 카드 형태. 이를 시안 A variant 로 교체. SITUATIONS 셀렉터/totalCount 표시 등 기존 기능 유지 + 시각만 변경. priority 유지.
- `app/match/page.tsx` — match-hero 이미지가 들어간 hero 섹션을 시안 C variant 로 교체. 기존 CTA/카피 유지 + 시각만 변경.

## Acceptance
- [ ] HomeHero.tsx 가 시안 A variant 형태로 렌더 (full-width + 카피 absolute overlay)
- [ ] match page hero 가 시안 C variant 형태 (광역 배경 그라데이션 + 중앙 카피)
- [ ] 모바일 (sm 이하) 에서 깨지지 않음 (text 가독성·이미지 잘림 확인)
- [ ] 한국어 alt 텍스트 유지
- [ ] PageSpeed LCP 적용 후 다시 측정 (홈만)
- [ ] PR 만들고 CEO 머지 요청

## 정리 (선택)
- design-preview/PACAA-626 라우트는 그대로 두기 OK (noindex, 향후 다른 시안 참조 가능). 또는 cleanup PR 별도. FE 판단.

## Branch 가이드
- main 에서 새 branch `feat/PACAA-626-hero-layout-apply` 권장
