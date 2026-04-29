---
name: "P1.4 — profile completeness audit (2주)"
assignee: "backend-engineer"
---

## 배경

[PACAA-70](/PACAA/issues/PACAA-70) P1.3 dedup + canonicalization 완료. `vendor_candidates`에 `dedup_status IN ('clean','merged')` 레코드 2,244건 확정.

## 목표

각 vendor_candidates canonical 레코드의 프로필 완전성(profile completeness)을 감사하여, 어떤 필드가 누락되어 있는지 파악하고 우선 보완 대상을 식별한다.

## 입력 데이터

- `vendor_candidates` WHERE `dedup_status IN ('clean','merged')` AND `deleted_at IS NULL` (2,244건)
- 필드: business_name, phone, address_raw, address_city, address_district, source_url, source_attribution

## 작업 범위

### Phase 1 — 필드 완전성 감사
- 카테고리 × 필드별 NULL 비율 집계
- 필수 필드: `business_name` (항상 있어야 함), `phone`, `address_raw`
- 선택 필드: `address_city`, `address_district`, `source_url`

### Phase 2 — 완전성 점수 산정
- 각 레코드에 completeness_score 산정 (필수 필드 충족률)
- 카테고리별 평균 completeness_score 집계

### Phase 3 — 보완 우선순위 결정
- completeness_score < 0.6 레코드 → 추가 enrichment 대상 플래그
- packlinx_db 소스지만 phone/address 누락 → 원본 DB 재조회 추천
- naver_place 소스지만 phone 누락 → 재스크랩 추천

## 산출물 (Definition of Done)

- `plans/profile_completeness_audit.py` 코드
- 카테고리별 필드 완전성 집계 리포트 (issue comment)
- completeness_score < 0.6 레코드 count per category
- P1.5 또는 enrichment 작업 인계 준비

## 의존성

- **선행 (충족):** [PACAA-70](/PACAA/issues/PACAA-70) P1.3 dedup 완료 ✅
- **CT
