---
name: "P1.2 — 8개 카테고리 vendor target list 수집 (2주)"
assignee: "backend-engineer"
---

## 배경

[PACAA-30](/PACAA/issues/PACAA-30) P1.1 분모 산출 시스템 완료로 게이트 조건 충족.
이제 8개 카테고리 각각의 **vendor target list** — 즉 Packlinx에 등록되어야 할 사업체 후보 목록 — 을 수집한다.

분모(사업체 수)는 이미  테이블에 저장되어 있다.
이 P1.2 작업의 결과가 numerator(실제 등록된 vendor 수)의 모수가 된다.

## 목표

8개 카테고리별로 **대한민국 포장재 공급업체 후보 목록** 수집 + Packlinx DB에 저장.

- 출처: 네이버 플레이스, 구글 비즈니스, 한국포장협회 회원사, 업종별 B2B 디렉터리 (엔터코리아, 지식산업센터 입주 목록 등)
- 수집 대상: 사업체명, 연락처, 주소, 대표 카테고리 (최소 필드)
- 중복 제거: P1.3 dedup pipeline으로 전달 (이 P1.2에서는 raw list 수집만)
- 저장:  테이블 (신규 설계 필요 — CTO sign-off)

## 카테고리 우선순위

Top-4 우선:
1. 골판지·종이박스 (분모: 1,000개)
2. 연포장재 (분모: 1,700개)
3. 라벨·스티커 (분모: 3,160개)
4. 인쇄·후가공 (분모: 17,558개)

Second-4 (병렬 인프라):
5. 플라스틱 용기·병 (분모: 2,100개)
6. 유리·금속 용기 (분모: 600개)
7. 포장 부자재 (분모: 3,425개)
8. 포장기계·자동화 (분모: 320개)

## 산출물 (Definition of Done)

- 8개 카테고리 각각에 대해 후보 사업체 목록 (raw, dedup 전)
- 각 레코드에 source_attribution (어디서 수집)
-  테이블 스키마 설계 + CTO sign-off + migration
- 수집 방법론 문서 (출처별 수집 방법, 필드 매핑)
- P1.3 dedup pipeline으로 넘길 준비 완료

## 의존성

- **선행 (충족):** [PACAA-30](/PACAA/issues/PACAA-30) P1.1 분모 산출 ✅
- **후속 게이트:** P1.3 (dedup+canonicalization)은 이 수집 후 시작
- **CTO 협업:** vendor_candidates 스키마 sign-off 필요

## Kill criterion

2주차 (2026-05-26) 시점에 8개 중 5개 카테고리 후보 목록 미수집 → CEO
