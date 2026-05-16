---
name: "[후속 PACAA-737] BE vendor_telesales_checks 파이프라인 실행 (2767건)"
assignee: "backend-engineer"
---

**부모**: PACAA-737 (보드 accept request_confirmation b38c793c). vendor 모델 분류 표현 최종 안 §B 데이터 시퀀싱 1단계.

## 목적
vendor 모델 분류의 1차 신호 데이터 채우기. 현재 `vendor_telesales_checks` 테이블 0건 (PACAA-515 마이그레이션 적용 후 파이프라인 미실행).

## Input
`companies` 2767건의 사업자등록번호 (BRN).

## Output
`vendor_telesales_checks` 테이블에 row 2767건 — 각 row 의 `result` 값:
- `found` → 통신판매업 신고 사업자 (Model B 신호)
- `not_found` → 미신고 사업자 (Model A 신호)
- `exempt` → 신고 의무 면제 (제조업·상시판매업 등) — 별도 처리 (배지 hide)

## 데이터 소스
공정위 통신판매사업자 공시 시스템. live API / 크롤링 / 다운로드 데이터셋 중 BE 가 적절 채널 선정 (속도/안정성/법적 검토).

## Acceptance
1. 2767건 모두 `vendor_telesales_checks.result` 채워짐 (NULL 0건)
2. 결과 분포 (found/not_found/exempt 카운트) + exempt 사유 top-N 본 이슈 코멘트로 보고
3. `checked_at` timestamp 채워짐
4. 재실행 가능한 idempotent 스크립트 (월간 재체크 위해)
5. 신뢰 못 할 source (예: 매칭 실패) 는 result 가 아닌 별도 error 로그로 분리 — 가짜 fill 금지

## Why high priority
PACAA-737 V1 UI 구현 (PACAA-XXX FE child) 의 1차 신호 의존. 본 child 완료 → CEO 가 결과 보드 보고 → 2단계 옵트인 컬럼 결정 → FE 실데이터 wire-up.

본 child done 시 CEO 자동 wake (parent_completed 트리거).
