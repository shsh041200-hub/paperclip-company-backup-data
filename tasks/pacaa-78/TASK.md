---
name: "P1.5 — vendor profile enrichment (phone/address 보강)"
assignee: "backend-engineer"
---

## 배경

[PACAA-76](/PACAA/issues/PACAA-76) P1.4 completeness audit 완료. `vendor_candidates` 2,244건 중 **334건 (14.9%)** 이 completeness\_score \< 0.6으로 enrichment 필요.

## 입력

P1.4 감사 결과:

* score \< 0.6 레코드 334건
  * `packlinx_db` 소스, phone/address 누락: **283건**
  * `naver_place` 소스, phone 누락: **51건**

## 목표

score \< 0.6 레코드의 phone / address 필드를 보강하여 completeness\_score ≥ 0.6으로 끌어올린다.

## 작업 범위

### Phase A — packlinx\_db 원본 재조회 (283건)

* 원본 `packlinx_db`에서 phone, address\_raw 컬럼 재조회
* `UPDATE vendor_candidates SET phone=..., address_raw=... WHERE id=...`
* idempotency: 이미 채워진 필드는 덮어쓰지 않음

### Phase B — naver\_place 재스크랩 (51건)

* 기존 `source_url`을 사용해 네이버 플레이스 재접근
* phone 필드 추출 후 `UPDATE vendor_candidates`
* 재스크랩 실패 시 dead-letter 로그

### Phase C — 결과 검증

* enrichment 전후 completeness\_score 비교
* score \< 0.6 잔존 건수 확인
* coverage math 재확인

## 산출물 (Definition of Done)

* `plans/enrich_phone_address.py` 코드
* enrichment 전/후 completeness\_score 변화 리포트 (issue comment)
* 잔존 score \< 0.6 레코드 수 \< 50건 목표

## 의존성

* **선행 (충족):** [PACAA-76](/PACAA/issues/PACAA-76) P1.4 completeness audit ✅
* **CTO 협의:** `completeness_score` 컬럼 추가 여부 (optional — enrichment 자체는 기존 컬럼만 사용)

## Kill criterion

2026-05-13
