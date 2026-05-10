---
name: "[FE] PACAA-452 Phase 2 batch 4 (final) — 공정·트렌드 4개 가이드 redesignVersion=1 + v1 슬롯 컴포넌트 추가"
assignee: "frontend-engineer"
---

## 목적

[PACAA-452](/PACAA/issues/PACAA-452) Phase 2 batch 4 CMO 콘텐츠 작성 완료 + [PACAA-453](/PACAA/issues/PACAA-453) Legal Counsel 자문 통과 후 FE 구현.

공정·트렌드 카테고리 4개 가이드 페이지에 v1 템플릿 슬롯(TL;DR·Callout·Checklist·FAQ·Sidebar·end-CTA)을 추가합니다.

## 콘텐츠 소스 (필수 확인)

**post-Legal 최종 확정 콘텐츠**: [PACAA-452 post-Legal 코멘트 #4a71471a](/PACAA/issues/PACAA-452#comment-4a71471a-a9a5-47f8-a19c-60e3686d1a90)

이 코멘트가 Legal PASS 확인 코멘트이며, 초안 원본은 [PACAA-452 초안 코멘트 #fbcd7e8b](/PACAA/issues/PACAA-452#comment-fbcd7e8b-9d8e-4368-ad22-81d7ed2d5ecb)에 수록되어 있습니다. CMO 워크스페이스 파일이 아닌 반드시 이 코멘트를 소스로 사용하세요.

## 대상 파일

`app/guides/[slug]/page.tsx` — GUIDES record 4개 수정

## 대상 슬러그 (4개)

1. `packaging-printing-guide` — 패키징 인쇄 공정 가이드
2. `packaging-machinery-guide` — 패키징 기계 가이드
3. `packaging-tape-comparison` — OPP·크라프트·무소음 테이프 비교
4. `2026-korea-packaging-trends` — 2026 한국 패키징 트렌드

## 작업 항목 (4개 가이드 공통 패턴)

각 가이드 entry에:
1. `redesignVersion: 1` 필드 추가
2. `body` 컴포넌트에 v1 슬롯 추가:
   - `<TldrBlock>` — 3개 bullet
   - `<CalloutBox>` — info / warn / tip (가이드별 3개)
   - `<ChecklistCard>` — 5개 항목
   - `<FaqSection>` — 4~5개 Q&A
   - `<SidebarGuides>` — 4개 관련 가이드
   - `<EndCta>` — title / subtitle / href

## Acceptance Criteria

- [ ] GUIDES rec
