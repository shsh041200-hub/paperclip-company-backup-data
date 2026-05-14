---
name: "P1 카테고리 hero 9장 생성 (Flux dev)"
assignee: "cmo"
---

## 부모: PACAA-702 (이미지 추가 후보 스카우팅)

보드 (a) P1 트랙 선택. `/categories/[slug]` 9개 카테고리 hero 이미지 신규 생성 + FE integration.

## 카테고리 9개 (정정: 보고서 6개 → 실제 9개)

`pkging-platform/data/categoryGuide.ts` grep 결과:
1. food-beverage
2. ecommerce-shipping
3. cosmetics-beauty
4. pharma-health
5. electronics-industrial
6. label-sticker
7. packaging-accessories
8. packaging-machinery
9. printing-postprocess

## 작업

### 1. 이미지 생성 (CMO 주도)
- **모델**: Flux dev (Replicate, PAYG)
- **장당 비용**: ~$0.04
- **총 비용**: 9 × $0.04 = **~$0.36** (보드 사전 승인 범위)
- **톤**: PACAA-626 directive = 실사 사진. 일러스트 X. 홈 hero 와 톤 일관.
- **사이즈/포맷**: 1600×900 webp (홈 hero 와 동일 spec). filename = `category-hero-{slug}.webp`.
- **저장 경로**: `pkging-platform/public/images/categories/`
- **프롬프트 가이드**: 산업 분위기 photo, 한국어 텍스트 오버레이 X (HTML 오버레이로), 깔끔한 스튜디오/공장/플랫레이 분위기.

### 2. FE integration (BE 또는 FE 위임)
- `/categories/[slug]/page.tsx` 에 hero 섹션 추가 (현재 텍스트만).
- `next/image` priority + sizes 적정값.
- 한국어 카테고리명 + 한 줄 설명을 hero 위 HTML 오버레이.
- SEO: alt 텍스트 한국어 ("식음료 패키징 업체 비교" 등).
- LCP 회귀 없는지 확인 (홈 hero 도입 시 측정한 baseline 대비).

### 3. acceptance
- [ ] 9장 webp `public/images/categories/` 커밋
- [ ] `/categories/[slug]/page.tsx` 9개 슬러그 모두 hero 렌더 라이브 (Vercel 배
