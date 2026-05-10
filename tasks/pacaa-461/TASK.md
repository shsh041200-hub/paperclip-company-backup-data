---
name: "[idle-improvement] /guides 검색 + chip 필터 동작 활성화 (PACAA-420 후속)"
assignee: "frontend-engineer"
---

## 목적
PACAA-420 종료 후 follow-up #1 — `/guides` 인덱스 페이지의 **검색 입력 + 카테고리 chip 필터** 가 현재 placeholder (input readOnly, chip 클릭 무동작). 클라이언트 사이드 만으로 동작 활성화.

라이브 현 상태: https://www.packlinx.com/guides

## 산출물

### 1. 검색 입력 활성화
- `<input readOnly>` → 일반 입력 가능
- 입력 시 모든 가이드 카드를 **title + summary 부분 문자열 매칭** (대소문자 무시·한글 공백 무시) 으로 필터링
- 0건 매칭 시 "검색 결과 없음" 빈 상태 메시지 (단순 텍스트)
- debounce 200ms 권장 (선택, 입력 매끄러움)

### 2. Chip 필터 활성화
- 카테고리 chip 6~7개 (전체 / 처음 발주 / MOQ 비교 / 친환경·ESG / 인쇄 품질 / 2026 트렌드 / 이사·물류) 모두 클릭 시 active state 토글
- chip 활성화 시 해당 카테고리 가이드만 표시
- "전체" chip = 필터 해제
- 검색 입력 + chip 필터 **AND 조합** (검색 결과 안에서 카테고리 또 좁힘)
- chip 분류 기준: 가이드 metadata 의 카테고리 + 또는 tag (lib/guide-data.ts 또는 [slug]/page.tsx GUIDES record 의 category 필드 활용)

### 3. URL 동기화 (선택, 없어도 OK)
- 검색어 + 활성 chip 을 `?q=...&cat=...` query string 으로 반영하면 공유 가능. 우선순위 낮음 — 시간 남으면 추가.

## 비대상 (out of scope)
- 백엔드 fulltext 검색 인덱스 (Algolia, MeiliSearch 등)
- 가이드 본문 검색 (오직 title + summary 매칭)
- 검색 분석/로깅
- 모바일 chip 가로 스크롤 UX (현재 wrap 처리로 충분)

## 작업 절차
1. `git pull origin main && git checkout -b feat/PACAA-457-guides-search-filter`
2. `app/guides/page.tsx` 만 수정 (다른 가이드 파일 무수정)
3. `'use client'` 컴포넌트로 검색·필터 state 분리 가능 (서버 컴포넌트 안에 client isl
