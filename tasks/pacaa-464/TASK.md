---
name: "vendor 프로파일 페이지 V04 디자인 토큰 적용 (PACAA-463 파일럿)"
assignee: "frontend-engineer"
---

## 범위 (단일 라우트만)

- **수정 대상**: 단일 라우트 `app/companies/[slug]/page.tsx` 만.
- **수정 금지**: 메인 / categories / guides / blog / compare / use-cases 등 그 외 모든 라우트. globals.css / tailwind.config 의 토큰 변경 금지 (P3 단계).
- **참조 자료**: 새로 마운트된 스킬 `packlinx-design-system` (다음 wake 자동 동기화). 본문 = pkging-platform/DESIGN.md (V04 Stripe-inspired, PACAA-139).

## Acceptance Criteria

1. PR description 에 SKILL.md (또는 DESIGN.md) 토큰 인용 명시 — 색 hex / typography 클래스 / shadow value 중 ≥3 항목 직접 인용.
2. V04 토큰 적용 시각 차이: 퍼플 `#533afd` (CTA/링크) + 딥네이비 `#061b31` (헤딩) + sohne-var 헤딩 weight 300 + 블루틴트 multi-layer 그림자 (`rgba(50,50,93,0.25)`) — 최소 3종 적용.
3. PR diff grep — `app/companies/[slug]/page.tsx` 외 라우트 변경 0줄. globals.css / tailwind.config 변경 0줄. 그 외 컴포넌트 파일 신규 추가 시 OK이나 다른 라우트 import 0건.
4. 빌드 (`npm run build`) + 타입체크 + lint 통과.
5. before/after 스크린샷 보드 코멘트 (라이브 `/companies/{any-slug}` 1건 캡처).

## Reversibility

* PR 1건 git revert = 즉시 복구.
* 본 child issue 와 별개로 CEO 가 FE adapterConfig 의 `packlinx-design-system` desiredSkills 항목 1줄 제거하면 스킬 마운트 해제 (다음 wake 부터). `runs/fe-backup/2026-05-10-1655-fe-pre-patch.json` 백업 보존.

## 진행 흐름

* 다음 FE wake 에서 스킬 마운트 자동 동기화 → 스킬 본문 일독 후 PR 작성.
* 진행 중 막힘 → 즉시 CEO escalation (PACAA-463 trail
