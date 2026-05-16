---
name: "[리뉴얼안 V2] vendor 상세 페이지 — 오늘의집/Houzz Pro Portfolio-first"
assignee: "ceo"
---

**목표**: 시각적 신뢰. 패키지 실물/시설 사진을 hero 로 전면.

**Benchmark**:
- https://ohou.se 전문가 (예: https://ohou.se/experts) 페이지
- https://www.houzz.com/professionals 임의 Pro profile

**WHAT 추출**:
- Hero: 풀폭 이미지 캐러셀 (실물/시설/팀, 4-6장)
- 전문 분야 칩 row + 한 줄 자기소개
- "최근 작업" 갤러리 그리드 (12-16칸, 클릭 lightbox)
- 우측 sticky: 프로필 카드 (사진/이름/연락처/응답시간)
- 하단 후기 (실리뷰 없으면 "첫 후기 작성" CTA — 가짜 후기 절대 금지)

**HOW (Packlinx 번역)**:
- 패키지 vendor → 실물 패키지/박스/기계 사진 (DB images 활용, 없으면 placeholder + "이미지 등록 요청" 안내)
- 시설 이미지 부재 시 카테고리 일러스트 또는 회색 placeholder + "이미지 미등록" 명시
- 톤: 오뉴얼집 친근체 X, 약간 격식 갖춘 B2B 친근체

**ANTI**:
- AI 생성 placeholder 이미지 금지 (보드 알레르기)
- 가짜 후기 카드 금지
- 빈 갤러리 = "공사중 GIF" 금지

**Deliverable**:
1. 라우트 `/internal/vendor-redesign/v2/[slug]` (noindex)
2. 실데이터 slug: `packaging_machinery-ac6b11ca` (이미지 부족할 경우 sample 1개 더 추가 sweep)
3. Vercel preview URL 을 본 이슈 코멘트로 회신
4. PR description 에 benchmark URL + 캡처 메모

**Acceptance**:
- Vercel preview 200, 모바일/데스크탑 반응형
- 이미지 없을 때 fallback UI 명시적
- 후기/별점은 "데이터 없음" 으로 표시 (가짜 X)
- noindex 확인
