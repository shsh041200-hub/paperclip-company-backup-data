---
name: "PACAA-490 P4 — guides (hub + 개별 가이드) UX/UI 개선"
assignee: "frontend-engineer"
---

## Context

부모: PACAA-490, P4. P3 companies 완료 후 트리거.

## 의도

guides = SEO acquisition 입구 + 전문성 시그널. 검색에서 가이드 → 신뢰 형성 → vendor list 진입 funnel. Packlinx 비전 "신뢰 기반 디렉토리" 의 백본.

## 작업 방식

P2 lean cycle, 단 hub + 개별 가이드 2종 동시:
1. 라이브 audit `/guides` (hub) + 대표 개별 가이드 2~3개
2. UX 갭 (콘텐츠 위계, 카테고리 grouping, 관련 vendor surface, 다음 가이드 추천, TOC, 모바일 reading)
3. 단일 개선안 preview `/design-preview/guides-hub-v1`, `/design-preview/guides-detail-v1`
4. CEO surface → 보드 confirm → production swap

## 포커스

- hub: 가이드 카테고리/주제 grouping, 인기·신규·가이드 picker, vendor cross-link
- 개별: TOC + 본문 가독성 + 인용 vendor surface + 다음 학습 path + breadcrumbs
- SEO 신호 (heading 위계, schema, breadcrumb)
- production /guides 라우트들 = 메인 next 우선순위 traffic 진입점

## Lock

- V05 토큰, 헤더/푸터 production 컴포넌트, /app/guides production 변경 0, noindex meta
- 메인 r3 V05 시각 어휘 일관성
- 가이드 contents 자체 수정 0 (UX/UI 만)

## 트리거

- P3 companies 완료 + 보드 swap accept → CEO 가 본 이슈 backlog → in_progress PATCH
- preview deploy → CEO Chrome surface
