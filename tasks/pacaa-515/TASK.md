---
name: "[Backend] PACAA-507 Phase B1 — is_verified=true 행 evidence audit + 미충족 false 마이그레이션 (LC §5)"
assignee: "ceo"
---

## 배경

[PACAA-507](/PACAA/issues/PACAA-507) Phase B 보드 승인 (CEO=owner, 즉시 발의). [PACAA-509](/PACAA/issues/PACAA-509) Legal Counsel 자문 §5 의 audit 권고 그대로 시행. `docs/legal/vendor-verification-criteria.md` (PACAA-510 머지 완료) 의 §1 부여 기준 5종 + §3 박탈 사유 7종 적용.

## Acceptance

### Step 1. evidence schema 라이브 introspect (memory `feedback_introspect_prod_schema_before_create.md`)

Supabase prod 에 다음 테이블/컬럼 존재 여부 확인 (예시):
- `vendor_brn_checks(vendor_id, status, checked_at, raw_payload)`
- `vendor_domain_checks(vendor_id, last_ok_at, status_code, redirect_chain)`
- `vendor_contact_checks(vendor_id, channel, confirmed_at, evidence_url)`
- `vendor_telesales_checks(vendor_id, brn, found_at)`
- (또는 동일 의미의 컬럼)

→ `to_regclass + information_schema.columns` 1회 GET. 결과:
- 모두 존재 + 데이터 채워져 있음 → Step 2 즉시 진행
- schema 부재 → Step 1b 분기 (아래)

### Step 1b. evidence schema 부재 시 분기 (사전 baked policy)

schema 가 없으면, 본 작업 1차로 **LC §1 5 종 기준에 대응하는 evidence 테이블 1회 마이그레이션 도입** + **현재 `is_verified=true` 행 전수에 대해 schema 만 만들고 행은 NULL** (즉 evidence 미보유 = audit 결과 false 로 강제).

schema 도입 시 회로 protection: PACAA-507 코멘트로 "schema 신규 도입 발견 — CEO 확인 후 다음 wake 진행" 알림 + status=blocked + blockedByIssueIds=[PACAA-507] 표시. **CEO 확인 후 진
