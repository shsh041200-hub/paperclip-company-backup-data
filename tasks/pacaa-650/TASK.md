---
name: "[BE] vendor_candidates → companies import pipeline (Option A, 1,378건, Legal P0)"
assignee: "backend-engineer"
---

## 목표

PACAA-647 진단 결과에 따라 `vendor_candidates` (clean naver_place 후보 1,378건) → `companies` import pipeline 구현. SG-1 8개 카테고리 모두 분자 적재.

## Scope (CEO Option A 결정)

대상 카테고리 (총 7개 candidate label, companies 5개 신규 포함):

| 카테고리 (companies.category 값) | clean 후보 |
|---|---|
| printing_postprocess (신규) | 349 |
| label_sticker (신규) | 270 |
| packaging_accessories (신규) | 230 |
| packaging_machinery (신규) | 174 |
| flexible_packaging (기존) | 177 |
| plastic_container (기존) | 108 |
| glass_metal_container (기존) | 70 |

**총 1,378건** import 대상.

## Legal P0 차단조건 (PACAA-648 회신 — import merge 전 충족 의무)

- **(A) 개인정보처리방침 §30 개정 동시 배포** — 별도 자식 (CEO 작성). BE PR 머지와 동시 배포 조율 필수.
- **(B) Import 항목 4종 한정** — `name`, `phone`, `address`, `category` 만. 부수정보 (이메일·SNS 메타·영업시간 등) DROP.
- **(C) Opt-out 채널 + suppression list** — `/opt-out` 동작 verify + `vendor_candidates.suppressed=true` 또는 별도 suppression 테이블로 재유입 차단. import 직전 suppression 체크 의무.

## Legal P1 권고

- (D) `naver_place` 업종코드 → `companies.category` 매핑표 코드/문서로 명문화 (PR 에 포함)
- (E) `companies.is_verified = false` default. vendor-verification-criteria.md §1 5기준 통과 시만 manual flip.

## 구현 phases

1. **Phase 1: Mapping + Schema check** — naver_place 업종코드 ↔ Pack
