---
name: "/match 페이지 5단계 위자드 확장 (PACAA-780 child)"
assignee: "ceo"
---

## 목적
`/match` 페이지를 3단계 → 5단계 위자드로 확장하여 사용자에게서 더 깊은 정보를 수집, 매칭 정확도 향상.

## 보드 승인 완료 (2026-05-17)
PACAA-780 interaction 4fcaf3ce — 옵션 'full' 선택.

## 변경 대상 파일
- `site/app/match/MatchClient.tsx` (메인 위자드 로직)
- `site/app/match/page.tsx` (필요 시 hero 카피만)
- `site/types/index.ts` (이미 material_type/packaging_form 존재)

## Step 구성 (새)

**Step 1** — 기존 업체 입력 (현행 유지)
- 변경: '직접 입력' 시 업종 선택을 선택→권장(asterisk), '건너뛰기' 후에도 다음 Step에서 업종 수집

**Step 2 (신규)** — 업종 선택 (단일)
- 9개 카테고리: 식품·음료/이커머스·배송/화장품·뷰티/의약·건강/전자·산업/라벨·스티커/인쇄·후가공/포장 부자재/포장기계·자동화
- Step 1에서 이미 업종 입력 시 prefill + skip 가능

**Step 3 (신규)** — 소재·형태 (멀티)
- 소재 그룹 (multi-select): 종이/플라스틱/비닐/금속/유리/친환경/기타
- 형태 그룹 (multi-select): 박스/파우치/병/캔/라벨/필름/완충재/기타
- "잘 모름" 옵션 제공 → 필터 미적용

**Step 4 (신규)** — 월 발주량 범위 (단일)
- 1천개 미만 / 1천~1만 / 1만~10만 / 10만 이상 / 모름

**Step 5** — 우선순위 기준 (최대 2개 선택)
- 4개 축: 낮은 MOQ / 빠른 납기 / 품질 인증 / 지역 근접
- 1순위 + 2순위 시각 구분 (1순위 70% 가중치)

**Step 6 (결과)** — Top 3 비교
- 현행 비교표 유지
- 1순위/2순위 행 highlight
- 필터링: 업종 + 소재/형태 매칭 후 가중치 정렬

## 추천 로직 (getRecommendations)
1. 업종 필터: industry_categories 교집합
2. 소재/형태 필터: 선택 항목 1개 이상 매칭 (선택 없으면 skip)
3. 발주량 필터: 사용자 발주량 >= vendor MOQ 인 것만 (모름 시 skip)
4. 가중치 정렬: 1순위 0.7 + 2순위 0.3
5. axis-data 없는 항목 사전 제거 (PA
