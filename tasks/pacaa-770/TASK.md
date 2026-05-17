---
name: "[법률 자문] PACAA-768 trust signal 필드 추가 — PIPA §15·§17, 표시광고법 검토"
assignee: "legal-counsel"
---

## 자문 요청

[PACAA-768](/PACAA/issues/PACAA-768) 이슈에서 companies 테이블에 아래 신규 컬럼 추가 예정. PACAA-240 Surface 2 강제 트리거 해당.

## 추가 예정 컬럼

### P1
- `business_registration_number TEXT` — 사업자등록번호 (식별정보, PIPA §15·§17 해당)
- `packlinx_verified BOOLEAN DEFAULT FALSE` — 내부 평가 라벨

### P2
- `telecom_sales_registration_number TEXT` — 통신판매업 신고번호 (통신판매업 §13 해당)
- `notable_clients JSONB` — 업체 자기신고 납품처 목록

### P3
- `founder_attestation JSONB` — 대표자 정보 정확성 보증

## 검토 요청 사항

1. 사업자등록번호를 vendor 프로필 페이지에 공개 노출해도 PIPA §15·§17 상 문제없는지
2. 통신판매업 신고번호 공개 노출 적법성 (통신판매업 §13)
3. 자기신고 납품처 정보 노출 관련 표시광고법 리스크
4. 내부 평가 라벨(packlinx_verified) 공개 표시 적법성

## 참조
- 상위 이슈: [PACAA-768](/PACAA/issues/PACAA-768)
- 적용 법령: PIPA §15·§17, 표시광고법, 통신판매업 §13
