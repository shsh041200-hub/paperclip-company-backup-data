---
name: "[리뉴얼안 V1] vendor 상세 페이지 — Alibaba/Made-in-China B2B Hard-data"
assignee: "ceo"
---

**목표**: 거친 정보 밀도 + 견적/문의 CTA 강세. 한국 B2B 구매자가 "이 업체 진짜인가" 1초 판단.

**Benchmark** (실제로 열어볼 것):
- https://www.alibaba.com 임의 Gold Supplier company profile
- https://www.made-in-china.com 임의 supplier 페이지

**WHAT 추출**:
- 좌: 회사 사진/로고 그리드 | 우: sticky 견적/문의 폼
- Above-fold: "Verified" 배지 + 사업연수 + 응답시간 + 인증 수치 박스
- 인증/특허 그리드 (썸네일)
- 생산능력/시설 수치 테이블
- 카탈로그 다운로드 PDF (없으면 "자료 요청" 폼)

**HOW (Packlinx 번역)**:
- "Verified" = 통신판매업번호 + 사업자등록번호 + 설립연도 박스화
- 시설 데이터 없으면 "정보 미제공" 명시 (가짜 채우기 금지)
- 인증 = 한국 KS/KC/ISO 등 실제 보유분만
- RFQ → 카톡채널 + 이메일 + 전화 (현재 founder 채널)

**ANTI**:
- 영문 카피 직역 금지 (한국 B2B 어색)
- 빈 필드 가짜 채우기 금지
- 별점/리뷰 노출 금지 (데이터 없음)

**Deliverable**:
1. 라우트 `/internal/vendor-redesign/v1/[slug]` (noindex, robots disallow)
2. 실데이터 slug: `packaging_machinery-ac6b11ca`
3. Vercel preview URL 을 본 이슈 코멘트로 회신
4. PR description 에 위 benchmark URL + 추출한 스크린샷/메모 첨부

**Acceptance**:
- Vercel preview URL 200 + 모바일/데스크탑 반응형
- 한국어 카피 자연스러움 (영문 직역 X)
- 빈 데이터 필드는 "정보 미제공" 또는 fallback UI
- meta robots noindex 확인
