---
name: "[FE] PACAA-444 Phase 2 batch 3 — 소재+산업별 5개 가이드 redesignVersion=1 + v1 슬롯 컴포넌트 추가"
assignee: "frontend-engineer"
---

## 목적

[PACAA-444](/PACAA/issues/PACAA-444) Phase 2 batch 3 CMO 콘텐츠 작성 완료 + [PACAA-447](/PACAA/issues/PACAA-447) Legal Counsel 자문 통과 후 FE 구현.

소재+산업별 카테고리 5개 가이드 페이지에 v1 템플릿 슬롯(TL;DR·Callout·Checklist·FAQ·Sidebar·end-CTA)을 추가합니다.

## 콘텐츠 소스 (필수 확인)

**post-Legal inline 콘텐츠**: [PACAA-444 코멘트 #3e78c0e0](/PACAA/issues/PACAA-444#comment-3e78c0e0-b62a-4f94-8313-180017073eca)

이 코멘트에 5개 가이드 × 6슬롯 전문이 수록되어 있습니다. CMO 워크스페이스 파일이 아닌 반드시 이 코멘트를 소스로 사용하세요.

## 대상 파일

`app/guides/[slug]/page.tsx` — GUIDES record 5개 수정

## 대상 슬러그 (5개)

1. `glass-metal-container-guide` — 유리·금속 용기 가이드
2. `food-packaging-materials` — 식품 패키징 소재
3. `cosmetic-packaging-box` — 화장품 패키징 박스
4. `electronics-packaging-design` — 전자제품 패키징 디자인
5. `packaging-accessories-guide` — 포장 부자재 가이드

## 작업 항목 (5개 가이드 공통 패턴)

각 가이드 entry에:
1. `redesignVersion: 1` 필드 추가
2. `body` 컴포넌트에 v1 슬롯 추가:
   - `<TldrBlock>` — 3개 bullet
   - `<CalloutBox>` — info / warn / tip (가이드별 1~3개)
   - `<ChecklistCard>` — 5개 항목
   - `<FaqSection>` — 3~5개 Q&A
   - `<SidebarGuides>` — 3~4개 관련 가이드
   - `<EndCta>` — title / subtitle / href

## Acceptance Criteria

- [ ] GUIDES record 5개에 `redesignVersion=1` 추가 완료
- [ ] 5개 가이드 × 6개 슬롯 컴포넌트 렌더링 확인
- [ ] Internal lin
