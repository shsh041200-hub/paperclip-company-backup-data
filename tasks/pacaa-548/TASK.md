---
name: "PACAA-490 P3 — companies/[slug] (vendor 상세) UX/UI 개선"
assignee: "frontend-engineer"
---

## Context

부모: PACAA-490, P3. P2 categories (PACAA-547) 완료 후 CEO 가 status=in_progress 트리거.

## 의도

Vendor 상세 페이지 = conversion 결정점. 구매자가 vendor list → 상세 진입 → 평가 → 다음 행동 (compare add / 연락처 확보 / 가이드 추가 학습).

## 작업 방식

P2 와 동일 lean cycle:
1. 라이브 audit `/companies/[slug]` (대표 vendor 3개로 audit — 데이터 풍부 / 빈 vendor / long tail)
2. UX 갭 식별 (정보 밀도, CTA 위계, trust 시그널, 모바일 fold, 다음 행동 surfaces)
3. 단일 개선안 preview `/design-preview/companies-v1`
4. CEO surface → 보드 confirm → production swap

## 포커스

- 정보 밀도 vs scannability — 메인 r3 의 monochrome density 패턴 따름
- 1차 CTA ("연락하기 / 견적 의뢰" 등 폐지 후 정렬) — production 의 현 의도 확인 후 reflect
- trust 시그널 (사업자 정보, 검증 timestamp, 출처 표시)
- 관련 vendor ("이 카테고리 다른 vendor") + 관련 가이드 surface
- 모바일 정보 위계 (limited screen 에 essential 만)

## Lock

- V05 토큰만
- 헤더/푸터 production 컴포넌트
- production `/app/companies/[slug]/page.tsx` 변경 0 (preview only)
- noindex meta
- 메인 r3 V05 시각 어휘 일관성

## 트리거

- P2 categories 완료 + 보드 production swap accept → CEO 가 본 이슈 status=backlog → in_progress PATCH
- preview deploy → 본 child 코멘트 → CEO Chrome surface
