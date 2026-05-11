---
name: "PACAA-490 FE r2 — 메인페이지 redesign v2 prototypes (layout shape axis, 보드 v3 피드백 반영)"
assignee: "frontend-engineer"
---

## 컨텍스트

부모: PACAA-490. 직전 iteration: PACAA-491 (PR #50, 보드 v3 reject).

r2 plan (단일 source of truth): `$AGENT_HOME/plans/PACAA-490-main-page-redesign.md` (CEO workspace, revisionId r2). FE 워크스페이스에 같은 path 미러본 없으면 본 description 이 대체 source.

## 보드 v3 피드백 (인용)

> 디자인 다시 바꿔야 해 색깔이 너무 다채로워 그리고 최근 검증된 업체기능은 필요없고 업체별 별점? 도 필요없어 그리고 인증마크가 너무 강조되었어 내용은 조금더 단순하고 그치만 디자인은 더 세련되고 그리고 상단바와 하단바도 글로벌 css색깔에 영향을 좀 받아야할거같고 지금 ui구조 자체가 너무 일렬이야 그냥 마냥 수직구조이기만해 이부분은 좀 다양한게 좋은듯 다시 디자인 개선안 3개를 만들어서 3창을 크롬에 띄워서 보여줘 그리고 내가 그중에 고르면 그때 작업 시작하는거야

## 산출물

1. **신규 PR** `feat/PACAA-490-main-redesign-v2-prototypes` (base: main, **신규 브랜치** — 기존 #50 별개)
2. **4 preview 라우트** (기존 r1 라우트는 같은 PR 에서 삭제):
   - `app/design-preview/main-r2-v1/page.tsx` — Editorial Asymmetric (60/40 split)
   - `app/design-preview/main-r2-v2/page.tsx` — Bento Modular (5칸 asymmetric grid)
   - `app/design-preview/main-r2-v3/page.tsx` — Sidebar Directory (좌 240px sticky + 우 main pane)
   - `app/design-preview/r2/page.tsx` — 3안 비교 인덱스 (layout shape 도식 + persona × 10초 mission 표)
3. 모든 preview 라우트 `metadata: { robots: 'noindex,nofollow' }` 필수
4. Vercel preview deploy URL 4개
5. **PR #50 close** (FE 가 close, comment 에 "v3 보드 피드백으로 r2 PR (#XX) 으
