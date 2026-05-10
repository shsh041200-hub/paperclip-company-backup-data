---
name: "PACAA-420 Phase 1 — 가이드 템플릿 컴포넌트화 + 인덱스 페이지 교체 + 1개 가이드 라이브 검증"
assignee: "frontend-engineer"
---

## 목적
PACAA-420 v1 목업 (보드 accept 완료) 을 실제 가이드 페이지에 적용하는 **Phase 1** — 템플릿/컴포넌트 인프라 + 1개 가이드 라이브 검증.

## 보드 accept 된 v1 목업 (참조)
- 인덱스: https://www.packlinx.com/mockups/guide-v2/index.html
- 디테일: https://www.packlinx.com/mockups/guide-v2/detail.html

## Phase 1 산출물 (이 ticket 범위)

### 1. 공유 컴포넌트 만들기 (`components/guide/` 신규)
v1 detail.html 의 디자인 토큰 + 컴포넌트를 그대로 React 화. 라이브 mockup 의 CSS 변수 (`:root` 블록) 와 클래스를 디자인 시스템으로 흡수:
- `<GuideHero />` — tag pill, title+subtitle, 메타바(저자·날짜·읽기시간·조회수), TL;DR 카드 슬롯
- `<GuideToc />` — 좌측 sticky 목차 (스크롤 동기화 — IntersectionObserver)
- `<GuideCallout variant="info|tip|warn">` — 콜아웃 박스
- `<GuideCompareTable />` — 컬러 pill 비교표 (`pillv` / `.warn` / `.good` 변형)
- `<GuideChecklist />` — 체크박스 리스트 카드
- `<GuideFaq />` — `<details>` accordion (open=true 첫 항목)
- `<GuideSidebar />` — 우측 sticky (vendor CTA + 공유 + related)
- `<GuideEndCta />` — 본문 끝 업체 비교 CTA

### 2. 인덱스 페이지 교체 (`app/guides/page.tsx`)
v1 mockup index.html 그대로 — Hero + 검색 + chip 필터 + featured 3카드 + 카테고리별 그리드 + 하단 CTA 스트립. 가이드 메타데이터(slug·title·summary·readTime·category·icon)는 기존 frontmatter / config 에서 읽어오기.

### 3. 1개 가이드 라이브 검증 — `corrugated-box-supplier-selection`
이 가이드 1개만 새 템플릿 적용해서 https://www.packl
