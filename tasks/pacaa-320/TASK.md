---
name: "비교 페이지 데이터 완성도 배지 (P0-3)"
assignee: "frontend-engineer"
---

## 목적

벤더 프로필 데이터 완성도를 비교 페이지에서 시각적으로 노출. 빈 셀(`—`) 누적 = 데이터 부재 vs 빈약 벤더 구분 불가 → 유저 의사결정 마찰 + 벤더 자가 보정 인센티브 미발동 (Vision 1축).

## Scope (S effort, ≤0.5d)

1. `lib/compare-data.ts` 또는 vendor 데이터 source 에서 18개 비교 필드 중 채워진 행 수 / 18 = `profile_completeness_pct` 계산 (server-side, build-time or runtime — 실시간 데이터 변동 없으면 build-time 권장).
2. `/compare` 페이지 vendor 컬럼 헤더에 "프로필 N%" 배지 표시. 75%↑ green / 50–75% amber / <50% gray + "벤더님 보강 필요" sub-text.
3. 빈 셀 `—` 는 회색조로 dim, 유저가 "데이터 없음" 임을 즉각 인지.
4. **trigger metric:** 배지 노출 후 vendor 자가 수정 요청 (`/contact` 또는 vendor portal) 도착 수. 4주 baseline.

## Out of scope

- 별도 ranking/score 노출. completeness ≠ quality, 혼동 금지.
- vendor 측 자동 알림 (이메일 푸시). 향후 vendor portal 인프라 깔리면 별도 ticket.

## Acceptance

- [ ] `/compare?ids=A,B,C` 라이브에서 3개 vendor 모두 배지 표시.
- [ ] 빈 셀 시각 차별화 (CSS 또는 컴포넌트).
- [ ] mobile 가로 스크롤 시에도 배지 sticky-readable.
- [ ] PR description 에 before/after 스크린샷 + completeness 계산 로직 1-paragraph.

## Pre-baked policies

- **막힘 24h+:** trigger absent → CEO escalation 코멘트 (`[ESCALATION → CEO]`). 보드 wake 대신 CEO 가 unblock.
- **데이터 source 모호:** `lib/compare-data.ts` 가 source-of-truth 인지 확인 후 모호하면 CEO 에 ask. 추측 코드 작성 금지.
- **PR 머지:** CEO 직접 confirm 불가, 보드 머지 권한.
