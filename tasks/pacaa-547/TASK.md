---
name: "PACAA-490 P2 — categories 페이지 UX/UI 개선 (audit + lean redesign)"
assignee: "frontend-engineer"
---

## Context

부모: PACAA-490 (사이트 전체 UX/UI 개선). 메인페이지 r3 사이클 V05 production ship 완료 (PR #55 머지). 보드 자율 권한 위임 (코멘트 8395934e, 2026-05-11 05:34 KST): "내가 따로 지시하지않아도 다음 페이지들을 다 픽해".

CEO 시퀀스 우선순위 — funnel 진입 빈도 + conversion 영향 기준:
1. **categories** (본 이슈, P2) — 메인 다음 funnel hub
2. companies/[slug] (P3) — conversion 결정점
3. guides (P4) — SEO acquisition 입구
4. faq (P5) — supportive polish
(compare 는 PACAA-498 별 stream)

## 작업 방식 — lean (r1~r3 multi-iteration 학습 후)

메인 r1~r3 사이클은 "3 direction prototype → 보드 픽 → r2 axis 재설계 → polish → ship" 으로 over-iteration. 본 이슈부터 lean:

1. 현재 페이지 라이브 audit + UX 갭 식별
2. **단일 개선안** prototype 1개 (3 direction 안 만들고 CEO+FE 판단으로 lead)
3. preview 라우트 deploy → CEO Chrome surface → 보드 confirm
4. 보드 OK 시 production swap, 추가 polish 요청 시 iteration 1~2회 cap

## 산출물

1. 라이브 audit: `/categories` 현재 구조 + UX 갭 식별 (메인 r1 baseline 캡처 패턴 따라)
2. 단일 개선안 preview 라우트 `/design-preview/categories-v1` (V05 token 적용, noindex)
3. 페이지 고유 UX 개선 포커스:
   - 카드 grid layout (현재 카테고리 5개 + vendor 수 표기 → 더 세련된 시각 위계)
   - filter ux (vendor 수, 인증, 지역 등 — 필요 시)
   - 카테고리 별 "무엇이 있는지" 미리보기 (vendor 일부 surface or 가이드 surface)
   - 메인페이지와의 일관성 (V05 token, 헤더/푸터, max-w-7xl) + 페이지 고유 차이
4. PR `feat/PACAA
