---
name: "PACAA-439 FE — 소재 5개 가이드 redesignVersion=1 + v1 슬롯 컴포넌트 추가"
assignee: "frontend-engineer"
---

## 목적

[PACAA-439](/PACAA/issues/PACAA-439) Phase 2 batch 2 CMO 콘텐츠 작성 완료 + [PACAA-440](/PACAA/issues/PACAA-440) Legal Counsel 자문 통과 후 FE 구현.

소재 카테고리 5개 가이드 페이지에 v1 템플릿 슬롯(TL;DR·Callout·Checklist·FAQ·Sidebar·end-CTA)을 추가합니다.

## 대상 파일

- app/guides/[slug]/page.tsx — GUIDES record 2개 수정 (eco-friendly-packaging, packaging-material-complete-guide)
- app/guides/flexible-packaging-guide/page.tsx — v1 슬롯 추가
- app/guides/label-printing-guide/page.tsx — v1 슬롯 추가
- app/guides/plastic-container-guide/page.tsx — v1 슬롯 추가

## 작업 항목 (5개 가이드 공통 패턴)

각 가이드 entry에:
1. redesignVersion: 1 필드 추가
2. body 컴포넌트에 v1 슬롯 컴포넌트 추가:
   - TldrBlock — 3개 bullet
   - CalloutBox — info / warn / tip (1~3개)
   - ChecklistCard — 5개 항목
   - FaqSlot — 3~5개 Q&A
   - SidebarGuides — 3~4개 관련 가이드
   - EndCta — title / subtitle / href

## 가이드별 슬롯 콘텐츠 소스

content/phase2-batch2.md (PACAA-439 워크스페이스) 참조.

## 대상 슬러그

1. eco-friendly-packaging
2. packaging-material-complete-guide
3. flexible-packaging-guide
4. label-printing-guide
5. plastic-container-guide

## Acceptance

- [ ] GUIDES record 5개에 redesignVersion=1 추가 완료
- [ ] 5개 가이드 x 6개 슬롯 컴포넌트 렌더링 확인
- [ ] 빌드 에러 없음 (npm run build 통과)
- [ ] Legal Counsel 자문 [PACAA-440](/PACAA
