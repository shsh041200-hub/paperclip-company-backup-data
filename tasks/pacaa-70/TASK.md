---
name: "P1.3 — dedup + canonicalization 파이프라인 (1주)"
assignee: "backend-engineer"
---

## 배경

[PACAA-38](/PACAA/issues/PACAA-38) P1.2 vendor target list 수집 완료로 게이트 조건 충족.
`vendor_candidates` 테이블에 ~3,103건 raw 레코드 (8개 카테고리, dedup_status='raw') 준비 완료.

## 목표

`vendor_candidates` raw 레코드에서 중복·이명 사업체를 제거하고 canonical record 확정.
이 작업 이후 `dedup_status IN ('clean','merged')` 레코드만이 coverage numerator 계산에 사용된다.

## 입력 데이터

- 테이블: `vendor_candidates` (~3,103건, dedup_status='raw')
- 소스: packlinx_db(1,396건) + naver_place(1,707건)
- 중복 패턴: 동일 사업체가 양 소스에 각각 등록되어 있을 가능성 높음

## 작업 범위

### Phase 1 — 자동 dedup (rule-based)
- 동일 `(category_id, business_name_normalized, phone)` → 자동 merge
- 동일 `(category_id, address_normalized)` 유사도 ≥ 0.9 → merge 후보 플래그
- normalized: 법인 접미사 제거 (주식회사/㈜/유한회사 등), 전화 형식 정규화

### Phase 2 — canonicalization
- packlinx_db 레코드를 canonical 우선 (실등록 데이터)
- naver_place 레코드가 추가 필드 보유 시 병합
- `canonical_id` self-ref FK 체인으로 duplicate 연결

### Phase 3 — 커버리지 검증
- 카테고리별 clean 건수 / 분모 = 실제 coverage %
- 라벨·스티커, 인쇄·후가공 커버리지 저조 → 추가 수집 여부 판단 트리거

## 산출물 (Definition of Done)

- dedup pipeline 코드 (`plans/dedup_pipeline.py` 또는 Edge Function)
- `vendor_candidates.dedup_status` 업데이트: raw → clean / merged / duplicate
- 카테고리별 clean 건수 집계 + coverage 계산 쿼리
- 처리 로그: 카테고리별 total_raw / merge
