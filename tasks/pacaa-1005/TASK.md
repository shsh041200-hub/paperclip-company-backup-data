---
name: "사이트 카피 lead 단어 '패키징' → '포장' 교체 (PACAA-1002)"
assignee: "frontend-engineer"
---

## 컨텍스트

PACAA-1002 보드 결정 (옵션 A accepted): 사이트 간판(TITLE/H1/META/nav)에서 lead 단어를 '패키징' → '포장'으로 교체. 본문/카테고리 라벨은 이미 '포장' 정렬되어 무변경. Packlinx 영문 브랜드는 유지.

근거: 우리 own SERP 캡처(PACAA-93)에서 포장 930회 vs 패키징 264회. 한국 B2B 표준 검색어 = '포장업체'.

## 작업 범위

### 변경 (간판만)

현재 라이브 사이트 확인된 위치:

1. **홈 (`/`) TITLE**: `전국 **패키징** 업체 찾기 — B2B 포장재 플랫폼 | Packlinx` → `전국 **포장** 업체 찾기 — B2B 포장재 플랫폼 | Packlinx`
2. **홈 META description**: `국내 1,396개 **패키징** 업체...` → `국내 1,396개 **포장** 업체...`
3. **/categories TITLE**: `**패키징** 카테고리 — 전국 포장재 업체 분야별 검색 | Packlinx` → `**포장** 카테고리 — 전국 포장재 업체 분야별 검색 | Packlinx`
4. **/categories H1**: `분야별 **패키징** 업체 찾기` → `분야별 **포장** 업체 찾기`
5. **/categories META description**: `식품·이커머스·화장품·의약·전자 등 분야별 전국 **패키징** 업체를 한눈에 비교하세요.` → `... 전국 **포장** 업체를 한눈에 비교하세요.`
6. **/about META description**: `국내 1,396개 **패키징** 업체...` → `국내 1,396개 **포장** 업체...`
7. **nav 메뉴 라벨**: `패키징 가이드` → `포장 가이드`

### 추가 sweep 필요 (위 외에도 grep)

- `/categories/[slug]` 카테고리 상세 페이지의 TITLE/H1/META
- `/vendors/[slug]` 벤더 상세 페이지 TITLE/H1/META
- `/guides/*` 가이드 페이지들의 TITLE/H1/META
- `/regions/*`, `/search`, `/match` 등 SEO 페이지 전수
- OpenGraph (`og:title`, `og:description`), Twitter Card 메타
- JSON-LD structured data (organizatio
