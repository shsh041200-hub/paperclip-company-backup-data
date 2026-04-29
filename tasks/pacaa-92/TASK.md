---
name: "PACAA-86 §6.2 — 키워드별 vendor density 매핑"
assignee: "backend-engineer"
---

## 산출물

50 키워드 × 카테고리별 vendor 매칭 카운트. 매칭 < 3 인 키워드는 랜딩 페이지에서 "카테고리 가이드 + claim CTA" 템플릿 fallback 적용.

## 결과 (2026-04-29 1차 실행)

소스: [PACAA-77](/PACAA/issues/PACAA-77) post-dedup vendor_candidates.

* 50 키워드 중 **49 키워드 ≥ 3 vendor 매칭** (정상 노출 가능)
* **1 키워드 fallback** (vendor < 3): `라벨링 머신 가격`
* 평균 vendor/키워드 = **65.2**

스크립트: `plans/keyword_density_pacaa86.py`. 출력: `plans/keyword_density_pacaa86.json`.

## DoD

1. 50 키워드 매칭 카운트 csv/json — done
2. fallback 키워드 식별 — done (1개)
3. §6.1 볼륨 검증 후 v1.1 키워드 셋 변경 시 1회 재실행

## Owner

Backend Eng. 본 이슈는 §6.1 의 v1.1 키워드 셋이 확정된 후 한 번 더 검증을 위해 in_progress 로 유지.
