---
name: "C1 Compare page (/compare/*) UX/UI 개선 — V05 일관성 + lean cycle"
assignee: "ceo"
---

## 배경

PACAA-490 시퀀스 5-페이지 100% closeout (2026-05-11T09:58Z). 보드 `f5df82d5` accept (12:48Z): **C1 — Compare page UX/UI 개선** 선택.

## 목표

`/compare/*` 페이지의 UX/UI 를 PACAA-490 sequence 의 V05 Stripe Purple 일관성 / lean cycle 패턴으로 개선.

## 작업 방식 — lean (P2~P5 패턴 동일)

1. 라이브 audit `/compare` + 대표 비교 URL (`/compare/{slug-A}-vs-{slug-B}` 류) UX 갭 식별
2. **단일 개선안** prototype (`/design-preview/compare-v1`) — 1축 commit
3. Vercel preview deploy
4. CEO Chrome surface (Before/After) + 보드 request_confirmation
5. 보드 accept → swap child → 머지 + production verify

## 핵심 axis (PACAA-490 sequence 학습)

- **V05 token bridge** — `--color-brand-500` (Stripe Purple) accent 일관 적용
- **CTA fold-above** — vendor 비교 후 다음 funnel 단계 (연락/견적) primary CTA hero 영역 노출
- **breadcrumb chevron** — P3/P4 와 일관
- **모바일 sticky CTA** — P3 패턴 적용

## Acceptance

- [x] FE audit + preview deploy
- [x] CEO Chrome surface + 보드 confirm interaction
- [x] Swap child 발의 + 머지 + production verify
- [x] V05 일관성 라이브 verify

## 트리거

- 즉시. FE 위임 (status=in_progress, priority=high).
- 보드 pick (`f5df82d5`) accept 가 mandate.

## 참고

- PACAA-490 sequence cycle 메트릭 (P2 65분 → P5 26분, learning 73% 단축). C1 cycle 예상 = 30~50분 (FE internalized).
- **C1 실제 cyc
