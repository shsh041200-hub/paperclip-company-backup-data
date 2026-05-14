---
name: "[BE] corrugated_box ENUM 누락 + 945 paper 회사 재분류 — SG-1 커버리지 0% 수정"
assignee: "backend-engineer"
---

## 문제

SG-1 커버리지 측정에서 `corrugated_box` 는 0건으로 집계됨.
실제로는 945개 `paper` 카테고리 회사들이 골판지박스 키워드에 서빙되고 있으나:
1. `category_type` ENUM에 `corrugated_box` 가 없음 (PACAA-650 migration에서 7개 신규 카테고리 추가 시 누락)
2. keyword_pages는 corrugated_box 키워드를 `paper` 로 매핑 → 745개 UI 서빙은 작동 중
3. label_sticker 키워드들도 `paper` 로 매핑 → `paper` 945건이 corrugated_box + label_sticker 혼재 가능

## 영향

- SG-1 corrugated_box 커버리지 = 0% (실제는 ~54% 이상 추정)
- 커버리지 대시보드 수치 전체가 왜곡됨
- CEO가 90% 목표 진행률을 정확히 파악 불가

## 작업 범위

### Step 1 — 분류 분석 (BE, dry-run)
`paper` 945건 샘플링 → name / subcategory / city 기반으로 corrugated_box vs label_sticker vs other 분류
예상: corrugated_box ~60–70%, label_sticker ~15–20%, other ~10–15%

### Step 2 — Schema migration (CTO sign-off 필요)
`ALTER TYPE category_type ADD VALUE IF NOT EXISTS 'corrugated_box';`
이미 PACAA-650 시 7개 추가했으나 corrugated_box 누락됨.

### Step 3 — Data migration (dry-run + CEO 승인)
분류 결과에 따라:
- 명확한 골판지박스 회사 → `corrugated_box`
- 명확한 라벨/스티커 → `label_sticker`
- 불명확 → `paper` 유지 (안전 기본값)
idempotency key + rollback SQL 포함.

### Step 4 — keyword_pages category 컬럼 업데이트
corrugated_box 키워드들: `paper` → `corrugated_box`
label_sticker 키워드들: `paper` → `label_sticker`
(UI 서빙 로직 변경 없음, 단순 FK 교체)

## DoD
- corrugated_box
