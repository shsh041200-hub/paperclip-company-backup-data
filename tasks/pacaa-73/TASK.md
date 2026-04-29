---
name: "PACAA-25 Goal 트리 패치 — SG-5 (buyer 경험 품질) + P5.1~P5.4 등록"
assignee: "ceo"
---

## 발의 경위

PACAA-72 plan v1 보드 사인오프 (2026-04-29 07:36 UTC, accepted).
§4-1 분기: PACAA-25 Goal 트리에 buyer 경험 축 (SG-5 + P5.1~P5.4)
신설.

## 작업 범위

1. **신규 SG 등록 (Vision 하위):**
   - SG-5: 8개 우선 카테고리에 진입한 buyer 의 머무름·행동 신호를
     정량화 가능한 수준으로 끌어올린다 (3~6개월).
   - 4 측정 신호 (목표값은 1주 baseline 후 보드 사인오프):
     * Bounce rate (8 카테고리 랜딩) Plausible — 12주 < 60% / Kill > 75% 4주 연속
     * Pages/session — ≥ 2.0 / Kill < 1.3 4주 연속
     * Action-rate (검색 → vendor 프로필 클릭, P2.3 click 퍼널) — ≥ 25% / Kill < 10% 4주 연속
     * 4주 재방문률 (Plausible cohort) — ≥ 8% / Kill < 3% 4주 연속

2. **신규 P 등록 (SG-5 하위 4개):**
   - P5.1: 8개 카테고리 랜딩 페이지 — first-impression 표준 (히어로/필터/가격대/대표 vendor 6개 카드). Owner: FE (페어 2 hire 후). 의존: P1.1~1.4 종료.
   - P5.2: 검색 결과 페이지 trust 신호 (인증 마크 / 거래 이력 / 응답률). Owner: FE + Backend Eng. 의존: P1.4.
   - P5.3: buyer self-action 입구 v0 (vendor 프로필 → 견적 문의 폼 1종, kakao/email 라우팅). Owner: FE. 의존: P5.1.
   - P5.4: 카테고리 콘텐츠 깊이 (카테고리당 1개 in-depth 가이드, ≥1500자). Owner: CMO. 독립.

3. **SG-3 메모 보강:**
   - P3.1~P3.4 신호 정의 시 SG-5 의 4개 측정 항목을 신호 후보로 포함하도록 명시 (CTO 검토 필요).

4. **PACAA-25 메모 업데이트:**
   - `memory/project_pacaa25_goal_tree_v1.md` 에 SG-5 + P5.1~P5.4 ID 추가.
   - Owner mapping 테이블 업데이트.

## P1.3 보호

- 본 패치는
