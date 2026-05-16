---
name: "[리뉴얼안 V4] vendor 상세 페이지 — Stripe/Linear Modern Minimal Trust"
assignee: "frontend-engineer"
---

**목표**: 여백 + 타이포 + 사실 밀도. "정돈된 신뢰" — 한국 B2B 변형 미니멀.

**Benchmark**:
- https://stripe.com/customers 임의 case study
- https://linear.app/customers 임의 페이지
- https://vercel.com/customers 임의 페이지

**WHAT 추출**:
- 큰 여백 + 모노크롬 (회색 90% + 1 accent)
- 헤더: vendor name (큼) + 한 줄 tagline + 작은 메타 (위치/설립)
- 본문: 3-4 정보 블록 (회사소개 / 주력 / 연락), 짧은 단락 + 굵은 키 fact
- 우측 사이드바 "Key facts" 6-8 항목 (설립년/직원/인증/카테고리/응답시간/위치)
- 푸터 위: 한 줄 카피 + 단색 큰 CTA 버튼

**HOW (Packlinx 번역)**:
- 폰트: Pretendard (이미 사용중)
- Accent: `--color-brand-500` (#533AFD V05 Stripe Purple)
- 톤: "쿨한 미니멀" X, "정돈된 신뢰감" O — 한국 B2B 구매자 위화감 회피
- 텍스트만으로 텅 비어 보이지 않게 — 한 장이라도 사진/일러스트 anchor 배치

**ANTI**:
- 영문 페이지 라이크 카피 직역 금지
- 사진 0장 = 너무 빈 인상 → 적어도 hero 1장 배치 (없으면 카테고리 일러스트)
- 미니멀 핑계로 정보 누락 금지 — 사실 밀도 유지

**Deliverable**:
1. 라우트 `/internal/vendor-redesign/v4/[slug]` (noindex)
2. 실데이터 slug: `packaging_machinery-ac6b11ca`
3. Vercel preview URL 을 본 이슈 코멘트로 회신
4. PR description 에 benchmark URL + 캡처

**Acceptance**:
- Vercel preview 200, 반응형
- 한국어 카피 자연스러움 (영문 직역 X)
- Key facts 사이드바 6+ 항목
- noindex 확인
