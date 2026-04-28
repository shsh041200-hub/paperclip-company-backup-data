---
name: "카테고리 개선: 패싯 필터 통합 (친환경/신선 boolean) + sitemap 갱신"
assignee: "cto"
project: "packlinx-website"
---

## 목표

패싯 필터 통합 + sitemap·검색콘솔 갱신.

## 범위

### 신규 패싯 필터 (모든 페이지 공통)

| 패싯 | 출처 | 노출 위치 |
|---|---|---|
| 소재 (material) | `MaterialType` 6종 (변경 없음) | 모든 페이지 |
| 인증 (cert) | `CertificationType` 17종, 카테고리별 그룹 (변경 없음) | 모든 페이지 |
| **친환경 여부** (boolean) | 신규 — `eco-special` 흡수 | 모든 페이지 |
| **신선·콜드체인** (boolean) | 신규 — `fresh_produce_packaging` 흡수 | `/industries/food-beverage` 우선 노출, 다른 페이지는 부가 |
| 사용처 (use_case_tag) | `use_case_tags` 테이블 (변경 없음) | 모든 페이지 |
| MOQ / 샘플 / 가격대 / 지역 | 기존 필터 유지 | 모든 페이지 |

### 구현 가이드

- 카테고리 페이지에 boolean 패싯 2개 추가 (친환경, 신선).
- URL 파라미터: `?eco=true&fresh=true` 추가 지원.
- DB:
  - `companies.is_eco` boolean 컬럼이 PACAA-15.2에서 추가됨 → 활용.
  - `companies.is_cold_chain` boolean 컬럼 신규 추가 (마이그레이션) — 기존 fresh_produce_packaging 보유 vendor를 일괄 true.
- 기존 `eco-special` 카테고리 페이지로 향하던 트래픽 (있다면) → `/categories?eco=true`로 301.
- sitemap 갱신:
  - `/products/*` 10개 + `/services/printing-design` 1개 신규 추가.
  - 제거된 3개 슬러그 제외.
  - 검색콘솔에 sitemap 재제출 (현재 봇 차단으로 외부 접근 막혀있을 수 있음 → 사이트 정상화 후 별도 진행).
- 패싯 필터 UI는 기존 `future-plans/2026-04-25-category-filter-redesign.md` v2 권고안(상단 드롭다운 필터 바)이 있으나, **이 티켓에서는 기존 UI 유지하고 boolean 2개만 추가.** 필터 바 재설계는 별도 티켓.

### 산출물

- 친환경/신선 boolean 패싯 동작 (URL 파라미터 + UI
