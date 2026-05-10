---
name: "가이드 페이지 P0 구현 — 카테고리 그루핑 + 카드 그리드"
assignee: "ceo"
---

## 가이드 페이지 P0 구현 — 카테고리 그루핑 + 카드 그리드

부모: [PACAA-404 — 가이드 페이지 개선안 제출](/PACAA/issues/PACAA-404). 보드 시안 승인 ("ok"), CEO 가 본 구현 child 발의.

### 시안 참고

- 첨부: `guides-mockup.html` (PACAA-404 첨부, attachmentId `dd42abf7-8485-4704-bf38-1511b6bdcf5f`)
- 시안 다운로드 후 브라우저로 열어서 시각 결과 그대로 재현이 목표 (Tailwind CDN inline → Next.js Tailwind v4 토큰으로 매핑)

### 변경 파일 (예상 3개)

#### 1. `lib/guide-data.ts`
- `GuideCategory` 타입 추가:
  ```ts
  export type GuideCategory = "box" | "material" | "industry" | "process" | "trend";
  ```
- `GuideMeta` 에 `category: GuideCategory` 필드 추가
- 20개 가이드에 카테고리 매핑 (시안 분류와 동일):
  - **box (6)**: shipping-box-pricing, corrugated-box-supplier-selection, corrugated-flute-types, small-quantity-custom-box, 이사박스-대량구매-가이드, 이사박스-사이즈-규격
  - **material (7)**: plastic-container-guide, flexible-packaging-guide, glass-metal-container-guide, label-printing-guide, packaging-accessories-guide, packaging-material-complete-guide, packaging-tape-comparison
  - **industry (4)**: food-packaging-materials, eco-friendly-packaging, cosmetic-packaging-box, electronics-packaging-design
  - **process (2)**: packaging-printing-guide, packaging-machinery-guide
  - **trend (1)**: 2026-korea-packaging-trends
- 카테
