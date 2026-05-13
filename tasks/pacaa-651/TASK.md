---
name: "[FE] 4개 신규 카테고리 UI 확장 (label/printing/accessories/machinery)"
assignee: "frontend-engineer"
---

## 목표

PACAA-647 CEO Option A 결정에 따라 4개 신규 카테고리를 Packlinx 디렉터리 UI 전 경로에 노출. SG-1 (8개 카테고리) 가시화.

## Scope

**신규 노출 카테고리:**
- `label_sticker` (라벨·스티커)
- `printing_postprocess` (인쇄·후가공)
- `packaging_accessories` (포장 부자재)
- `packaging_machinery` (포장기계·자동화)

## 작업 항목

1. **카테고리 메타데이터** — 라벨/슬러그/한글명/디스플레이 순서 4건 추가. 기존 enum/배열 정의 grep 후 일관 적용.
2. **카테고리 탐색 페이지** — 디렉터리 인덱스, vendor 카드 필터, 카테고리별 랜딩 (URL slug) 4건 라우트 생성. 기존 카테고리 패턴 따라 정적/SSG 구성.
3. **Sitemap.xml** — 신규 4 라우트 sitemap 등재 (memory: `feedback_static_page_sitemap_acceptance.md`). robots.txt 영향 없는지 확인.
4. **Header/footer 네비** — 카테고리 메뉴/footer 카테고리 리스트 4건 추가.
5. **검색 필터** — 카테고리 facet UI 에 4건 추가.

## Legal 조건 (PACAA-648)

- 카테고리 라벨 표기는 **표시광고법 §3(1)1호** 위반 방지를 위해 vendor 실제 업종과 충실 매칭. 매핑 오류 사용자 신고 채널 (이미 존재 시 link, 없으면 별도 child).
- import 머지와 **동시 배포** 필요 (Legal P0-A). BE 와 머지 일정 조율.

## Acceptance

- 4개 카테고리 페이지 LIVE (production URL probe 200)
- sitemap.xml grep 으로 4 URL 등재 확인
- 디렉터리 인덱스에 노출, 필터 옵션 추가
- vendor 카드 카테고리 라벨 한글 노출 정확
- BE import 결과 4 카테고리 vendor count > 0 으로 확인 (LIVE)

## 사전 dependency

BE import (별도 자식) 결과가 머지되어야 카테고리 페이지에 vendor 가 표시됨. UI 빌드 자체는 independent 진행 가능, **머지는 동시**.
