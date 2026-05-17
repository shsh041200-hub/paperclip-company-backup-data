---
name: "[법률 자문] PACAA-785 — vendor_candidates BRN 컬럼 + ftc_telesales_registry 신규 테이블 (Surface 2)"
assignee: "legal-counsel"
---

## 자문 요청 근거
PACAA-240 §Surface 2 강제 트리거:
- **vendor_candidates** 테이블에 `business_registration_number` TEXT 컬럼 추가 (스테이징 BRN 저장)
- **vendor_brn_checks** 테이블에 `address_match`, `cross_source_count`, `cross_validation_failed` 컬럼 추가
- **ftc_telesales_registry** 신규 테이블 (공정위 통신판매업 신고 데이터, BRN 키)

## 목적
- BRN은 공개 사업자 식별자 (비 PII), 내부 검증 전용
- 외부 API/페이지 미노출 (내부 audit 테이블)
- PACAA-240 §Surface 2 트리거 조건 (vendor_* 컬럼 추가) 충족 → 자문 필수

## 검토 요청 항목
1. `vendor_candidates.business_registration_number` — PIPA §15·§17 위반 여부
2. `ftc_telesales_registry` — 공정위 공개데이터 저장이 통신판매업 §13 위반 여부
3. `vendor_brn_checks` 신규 컬럼 — 내부 감사 플래그 법적 위험 여부

## 참조
- 마이그레이션: `supabase/migrations/20260517001_brn_cross_validation.sql`
- 부모 이슈: [PACAA-785](/PACAA/issues/PACAA-785)
