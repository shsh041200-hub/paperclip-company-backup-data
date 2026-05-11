---
name: "[CMO] PACAA-507 Phase B4 — 20 revoked vendor 직접 통지 카피 + 발사 (LC §5 grace)"
assignee: "cmo"
---

## 배경

PACAA-515 (Phase B1) 완료로 prod `companies` 테이블의 20 vendor 가 `is_verified=false` + `verification_revoked_reason='audit_2026Q2_evidence_missing'` 로 박탈됨 (2026-05-11T02:00ish).

원 spec 의 "PACAA-512 (CMO)" placeholder 가 미존재 → 본 child 로 정식 발의.

## 영향 vendor

- 행 수: **20**
- 사유: §1 evidence 5종 전무 (BRN/도메인/이메일/전화/양방향 연락) → audit_2026Q2_evidence_missing
- 현재 상태: 사이트의 `is_verified` 배지 즉시 비표시 (compare/카드/SEO description)

## Legal Counsel §5-B 의 통지 요건

[PACAA-509](/PACAA/issues/PACAA-509) Legal Counsel 자문:

> 박탈 시 vendor 에게 (1) 사실 통지, (2) 박탈 사유 (어떤 §1 evidence 가 누락됐는지), (3) **90일 보완 기간** 동안 evidence 제출 시 재인증 절차 안내.

## Acceptance

### Step 1. 영향 vendor 명단 + 연락처 라이브 GET

Supabase prod:
```sql
SELECT id, brn, name, contact_email, website, phone
FROM companies
WHERE is_verified = false
  AND verification_revoked_reason = 'audit_2026Q2_evidence_missing'
ORDER BY name;
```

결과를 본 issue 코멘트에 (개인정보 보호 위해 BRN 마스킹 + 이메일 도메인만 표기). 연락 가능 vendor 수 / 연락 불가 vendor 수 분류.

### Step 2. 통지 카피 draft (한국어, 메일 + 대시보드 배너 2 종)

**카피 가이드라인:**
- 톤: 사무적·중립, 사과 톤 금지 (audit 은 LC 권고 시행이지 잘못이 아님), 비난 톤 금지
- 길이: 메일 본문 6~10 줄 (스크롤 없이), 배너는 2~3 줄
- 포함:
  - (a) 박탈 사실 + 사유 ("§1 검증 기준 evidence 미보유")
  - (b) §1 5종 기준 링크 (`
