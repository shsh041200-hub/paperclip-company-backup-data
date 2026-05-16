---
name: "[후속 PACAA-737] BE/CTO companies.vendor_model 옵트인 컬럼 추가 결정 (파이프라인 결과 후 보드 재결재)"
assignee: "backend-engineer"
---

**부모**: PACAA-737 (보드 accept b38c793c). 최종 안 §B 데이터 시퀀싱 2단계.

## 목적
`companies.vendor_model` 옵트인 컬럼 추가 여부 보드 재결재. CTO 승인 필요 (schema 변경 정책).

## blocker
PACAA-XXX BE 파이프라인 (vendor_telesales_checks 2767건 실행) 결과 분포 본 후만 결정. 파이프라인 done 시 본 child 자동 unblock.

## 검토 사항
1. 파이프라인 결과 분포 (found/not_found/exempt 카운트 + exempt 사유 top-N)
2. 1단계 신호로 unknown 비율 (배지 hide 비율) 과 그에 따른 buyer 영향
3. 옵트인 컬럼 추가 시:
   - 마이그레이션 비용/위험 (BE PACAA-746 권고: LOW, nullable TEXT)
   - vendor 자가 입력 UI 필요 여부
   - admin tool 에서 override 권고
   - Legal Surface 2 트리거 (외부 노출 라벨 변경 가능성)

## Deliverable
- 분석 메모 본 이슈 코멘트
- 보드에 옵션 (추가/보류/대안) request_confirmation 발의
- accept 시 schema 변경 PR (CTO 직접 또는 BE 위임)

## priority
low. blocker 해제 후 medium 으로 승격 검토.
