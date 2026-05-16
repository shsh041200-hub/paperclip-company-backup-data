---
name: "[리뉴얼안 V5] vendor 상세 페이지 — Naver Place / 다나와 Korean Discovery"
assignee: "frontend-engineer"
---

**목표**: 한국 B2B 구매자가 매일 보는 UX 컨벤션. 친숙도 극대화.

**Benchmark**:
- https://map.naver.com 임의 place card (지도 + 정보 + 메뉴 + 연락처)
- https://kr.kakaomap.com 임의 place
- https://www.danawa.com 임의 비교 페이지
- https://www.gmarket.co.kr seller profile

**WHAT 추출**:
- 좌상단: 작은 지도 (Kakao/Naver) + 위치 핀
- 우: 빠른 정보 패널 (전화/카톡/문의/길찾기 4 버튼)
- 탭 구조: 홈 / 회사정보 / 취급품목 / 문의 (모바일 first)
- 같은 카테고리 vendor 3개 한눈에 비교 mini-card 슬라이드
- 모바일 하단 sticky: "지금 문의하기" full-width 버튼

**HOW (Packlinx 번역)**:
- 지도: Kakao Static Map (무료, API key 없으면 OpenStreetMap embed)
- 동료 vendor 3개 = `same category, exclude self, limit 3` 쿼리
- 전화 = `tel:` (founder 번호는 이미 사이트 footer 공개)
- 카톡 = `https://pf.kakao.com/...` (현재 채널 없으면 이메일로 대체)
- 카테고리 컨벤션 한국 친숙: 햄버거 메뉴 X, 명시적 탭

**ANTI**:
- 영문 미니멀 컨벤션 (햄버거, 미니 hero) 금지
- 지도 fallback 없이 빈 회색 박스 금지
- 좌표 없는 vendor → 시/구 단위 텍스트 fallback (지도 영역 자체 hide)

**Deliverable**:
1. 라우트 `/internal/vendor-redesign/v5/[slug]` (noindex)
2. 실데이터 slug: `packaging_machinery-ac6b11ca`
3. Vercel preview URL 을 본 이슈 코멘트로 회신
4. PR description 에 benchmark URL + 캡처

**Acceptance**:
- Vercel preview 200, 모바일 우선 + 데스크탑
- 지도 표시 또는 명시적 fallback
- 동료 vendor 3개 카드 실데이터
- noindex 확인
