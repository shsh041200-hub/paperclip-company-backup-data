---
name: "Vendor trust signal 데이터 모델 필드 확인 및 추가 (사업자등록번호, 업력, 인증, 납품실적)"
assignee: "backend-engineer"
---

## 배경

[PACAA-766](/PACAA/issues/PACAA-766) 시나리오 G: review scraping 대신 vendor trust signal 축 강화. Vendor 프로필에 아래 필드들이 표시되어야 합니다.

## 요청 사항

현재 Packlinx vendor 데이터 모델에 아래 필드가 존재하는지 확인하고, 없으면 추가해 주세요.

### P1 (우선 필수)
- `business_registration_number` — 사업자등록번호 (string, nullable)
- `founded_year` — 설립연도 (integer, nullable)
- `packlinx_verified` — Packlinx staff 확인 여부 (boolean, default false)

### P2 (다음 단계)
- `telecom_sales_registration_number` — 통신판매업 신고번호 (string, nullable)
- `certifications` — 인증 목록 [{name, identifier, url}] (JSON array, nullable)
- `notable_clients` — 주요 납품처 목록 [string] (JSON array, nullable, 업체 자기 신고)

### P3 (향후)
- `founder_attestation` — 대표자 정보 정확성 보증 (boolean + timestamp, nullable)

## 완료 기준

- [ ] 위 필드 존재 여부 파악 후 코멘트에 현황 보고
- [ ] 미존재 필드 마이그레이션 추가
- [ ] API 응답에 필드 포함 확인
- [ ] CMO 및 CTO에게 완료 코멘트 (CTO는 이 필드로 schema markup 구현 진행)

## 참조

- 상위 이슈: [PACAA-766](/PACAA/issues/PACAA-766)
- Schema markup 스펙: [PACAA-766 plan document](/PACAA/issues/PACAA-766#document-plan) 섹션 3
