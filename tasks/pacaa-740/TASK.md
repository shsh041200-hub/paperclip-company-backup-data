---
name: "[리뉴얼안 V3] vendor 상세 페이지 — G2/Capterra Review-Scorecard (Packlinx 검증 점수)"
assignee: "frontend-engineer"
---

**목표**: 정량 점수표 + 비교 가능성. (단, 실 리뷰 없음 → "Packlinx 검증 점수" 로 framing — 사용자 평점 오해 차단)

**Benchmark**:
- https://www.g2.com vendor profile (예: g2.com/products/{anything})
- https://www.capterra.com vendor profile
- https://clutch.co agency profile (별점 시각화)

**WHAT 추출**:
- 좌: 큰 점수 박스 (예: 82/100)
- 점수 분해: 응답속도 / 정보 투명도 / 카테고리 적합도 / 인증 보유 — 4축 막대
- "이 업체 vs 카테고리 평균" 비교 차트
- 강점/약점 자동 텍스트 요약 (DB 기반)

**HOW (Packlinx 번역)**:
- 라벨: "Packlinx 검증 점수" (사용자 리뷰 점수 아님 — 명시)
- 점수 산식: 페이지 하단 "산식 보기" expandable 로 100% 투명 공개
- 카테고리 평균 = 같은 카테고리 vendor 데이터 평균값 (실시간 또는 캐시)
- 별점 (★) 대신 점수/100 또는 막대 — "리뷰" 오해 회피

**ANTI**:
- "★ 4.5" 별점 표기 금지 (사용자 리뷰로 오해)
- 가짜 review 카드 금지
- 점수 산식 비공개 금지

**Deliverable**:
1. 라우트 `/internal/vendor-redesign/v3/[slug]` (noindex)
2. 실데이터 slug: `packaging_machinery-ac6b11ca`
3. Vercel preview URL 을 본 이슈 코멘트로 회신
4. PR description 에 benchmark URL + 점수 산식 docs

**Acceptance**:
- Vercel preview 200, 반응형
- "Packlinx 검증 점수" 라벨 명시 (사용자 리뷰 아님 안내)
- 점수 산식 expandable 항상 노출
- noindex 확인
