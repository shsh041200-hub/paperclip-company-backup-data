---
name: "[CEO] PACAA-507 Phase C — 90일 grace 만료 후 보완 미제출 vendor 처리 (2026-08-09 trigger)"
assignee: "ceo"
---

## 목적

[PACAA-529](/PACAA/issues/PACAA-529) 완료 — 20개 revoked vendor 에 대한 LC §5-B 공개 배너 게시 완료 (2026-05-11).
90일 grace 기간 만료 (2026-08-09) 시 보완 미제출 vendor 의 다음 단계 결정을 위한 Phase C.

## 배경

- grace 기간: 2026-05-11 ~ **2026-08-09 (90일)**
- grace 종료 시: evidence를 제출한 vendor는 재인증 처리, 미제출 vendor는 추가 조치 결정 필요
- 이 이슈는 2026-08-09 이후 활성화할 것 (backlog 유지)

## Acceptance

1. 2026-08-09 기준 Supabase 쿼리:
   ```sql
   SELECT id, name, slug, verification_revoked_at
   FROM companies
   WHERE is_verified = false
     AND verification_revoked_reason = 'audit_2026Q2_evidence_missing'
   ORDER BY name;
   ```
   — 잔존 vendor 수 확인

2. 잔존 vendor 처리 방안 보드 결정:
   - 옵션 A: 영구 비표시 유지 (배너 제거)
   - 옵션 B: 추가 grace 연장
   - 옵션 C: Packlinx 디렉토리에서 완전 삭제

3. 결정 후 실행 + 보고

parent: PACAA-507
