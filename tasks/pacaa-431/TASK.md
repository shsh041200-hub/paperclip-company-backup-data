---
name: "PACAA-428 FE — 박스·골판지 5개 가이드 redesignVersion=1 + v1 슬롯 컴포넌트 추가"
assignee: "frontend-engineer"
---

## 목적

[PACAA-428](/PACAA/issues/PACAA-428) Phase 2 batch 1 CMO 콘텐츠 작성 완료 + [PACAA-430](/PACAA/issues/PACAA-430) Legal Counsel 자문 통과 후 FE 구현.

박스·골판지 카테고리 5개 가이드 페이지에 v1 템플릿 슬롯(TL;DR·Callout·Checklist·FAQ·Sidebar·end-CTA)을 추가합니다.

## 대상 파일

`app/guides/[slug]/page.tsx` — GUIDES record 5개 수정

## 작업 항목 (5개 가이드 공통 패턴)

각 가이드 entry에:
1. `redesignVersion: 1` 필드 추가
2. `body` 컴포넌트에 v1 슬롯 컴포넌트 추가:
   - `<TldrBlock>` — 3개 bullet
   - `<CalloutBox>` — info / warn / tip (1~3개)
   - `<ChecklistCard>` — 5개 항목
   - `<FaqSection>` — 3~5개 Q&A
   - `<SidebarGuides>` — 3~4개 관련 가이드
   - `<EndCta>` — title / subtitle / href

## 가이드별 슬롯 콘텐츠 소스

`content/phase2-batch1.md` (PACAA-428 워크스페이스) 참조.

## 대상 슬러그

1. `corrugated-flute-types`
2. `shipping-box-pricing`
3. `small-quantity-custom-box`
4. `이사박스-사이즈-규격`
5. `이사박스-대량구매-가이드`

## Acceptance

- [ ] GUIDES record 5개에 `redesignVersion=1` 추가 완료
- [ ] 5개 가이드 × 6개 슬롯 컴포넌트 렌더링 확인
- [ ] 빌드 에러 없음 (`npm run build` 통과)
- [ ] 라이브 verify 후 PACAA-428에 완료 코멘트
