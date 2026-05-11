---
name: "PACAA-490 R3-D — V05 production swap + 11 preview 폴더 정리 + hex→token"
assignee: "frontend-engineer"
---

## Context

PACAA-496 r3 단계 종료. 보드 픽: **V05 상황별 온보딩 플로우** (CMO 1·2·3위 외 픽 — 채널톡 톤 컨버전 우선 컨셉). PR #54 (`feat/PACAA-496-r3-10-variants`) 머지는 보드 직접 (CEO 권한 외).

상위 단계: PACAA-490 메인페이지 redesign 마지막 단계 — V05 production swap + 11 preview 폴더 정리 + 토큰화.

## V05 컨셉 spec (CMO brief PACAA-495 / Part 2 V05)

- **Hero**: 단순 질문형. "포장재 파트너를 찾고 계신가요?" 대형 타이포 + 상황 카드 3개 (처음 구매 / 공급사 변경 / 대량 견적)
- **1차 IA**: 질문 headline → 상황 선택 카드 3개 → [선택 후] 맞춤 카테고리·업체 필터 결과
- **2차 IA**: 일반 카테고리 browse → 가이드 콘텐츠 → footer
- **CTA**: 각 상황 카드 클릭 = 온보딩 CTA / 헤더 `전체 업체 보기` 탈출 경로
- **차별점**: 바이어 상황을 platform이 먼저 파악. 첫 방문 전환율 최적화

라이브 prototype: `/design-preview/main-r3-v05` (PR #54 Vercel preview)
구현 파일 참고: `app/design-preview/main-r3-v05/MainR3V05Client.tsx` (160줄)

## 작업 범위 (단일 PR)

### 1. PR #54 머지 대기 (보드 직접)

R3-D 작업은 PR #54 가 main 에 머지된 후 시작. 머지되지 않았다면 본 child blocked.

### 2. V05 → production swap (필수)

- `app/page.tsx` 를 V05 컨셉 기반으로 재작성 (현재 production 디자인 폐기)
- `'use client'` 분리 필요 시 `app/HomeClient.tsx` 등 분리 (V05 는 useState 사용 → 클라이언트)
- noindex/robots metadata 제거 (production = 색인 필수)
- 헤더의 "Packlinx" 로고 링크 `/design-preview/main-r3` → `/` 로 교체
- 상황 카드 link: V05 prototype 의 `/?industry=corrugated`, `/?moq=1000` 등 qu
