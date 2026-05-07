---
name: "[Idle-improvement #2] vendor 비교 테이블 — implementation"
assignee: "frontend-engineer"
---

## 배경

PACAA-265 spec accept 됨 (보드 채택 9894f603). 본 이슈는 implementation 단계.

Spec: PACAA-265 코멘트 595cf496 (전체 와이어프레임 + 18필드 + MVP 스콥).

## 작업

Vendor 비교 테이블 MVP 구현. spec 그대로 따라가되, 의문점은 즉시 코멘트로 surface.

### Scope

1. **벤더 카드 — "비교에 추가" 버튼**
   - 위치: `src/app/categories/[slug]/page.tsx` 의 vendor card
   - 클릭 시 localStorage 기반 비교 카트에 추가

2. **비교 카트 (하단 고정 드로어)**
   - 최대 3개 vendor
   - localStorage persistence (key: `packlinx_compare_cart`)
   - 모바일 375px / 데스크톱 모두 동작
   - 2개 이상 시 "비교하기" CTA 활성화

3. **`/compare?ids=slug-a,slug-b[,slug-c]` 페이지 (SSR)**
   - Next.js App Router page.tsx
   - `<meta name="robots" content="noindex">` 필수
   - SSR: slug array → companies 테이블 IN 쿼리
   - 비교 테이블 (텍스트/배지, 차트 없음)
   - 각 vendor 컬럼 하단 "프로필 보기" / "문의하기" CTA

4. **벤더 프로필 페이지 — "비교에 추가" 버튼**
   - `src/app/companies/[slug]/page.tsx`
   - 비교 카트 toggle

### 비교 필드 (spec 기준 18개)

spec PACAA-265#595cf496 의 "데이터 모델 후보" 표 그대로.

## Acceptance

- [ ] 카테고리 목록의 vendor card 에 "비교 추가" 버튼 동작
- [ ] 비교 카트 localStorage persistence (페이지 리로드 후 유지)
- [ ] 모바일 375px + 데스크톱 1280px 양쪽 비교 카트 정상
- [ ] `/compare?ids=...` SSR 페이지 — 1/2/3 vendor 모두 렌더
- [ ] noindex meta tag 적용
- [ ] 벤더 프로필에서도 비교 추가 가능
- [ ] 모바일 비교 페이지 sticky 첫 컬럼 + h
