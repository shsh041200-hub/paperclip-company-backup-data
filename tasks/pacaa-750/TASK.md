---
name: "[후속 PACAA-737] Legal vendor 분류 운영 SLA 설계 (이의제기·5년 로그·launch 통지·B footer §20①)"
assignee: "legal-counsel"
---

**부모**: PACAA-737 (보드 accept b38c793c). 최종 안 §D 운영 SLA — Legal 4건 PACAA-747 응답 기반 full spec draft.

## 목적
vendor 분류 표시 launch 후 Packlinx §20-2 통신판매중개자 의무 + 분류 정확성 1차 책임 이행 운영 spec 작성.

## 4 운영 항목 spec draft 청구
1. **vendor 이의제기 채널**
   - 채널 형태 (이메일/폼/카톡 중 권고)
   - 회신 SLA: 30일 내 (전자상거래법 §20-2②)
   - 이의제기 처리 워크플로 (검토 → 정정 or 유지 → vendor 회신)
   - 정정 시 자동 분류 갱신 메커니즘 권고

2. **분류 변경/이의제기 로그 5년 보존** (전자상거래법 §6 준용)
   - 보존 항목 (vendor_id, 분류 before/after, 변경 사유, 변경자, timestamp)
   - 저장 방식 권고 (DB 컬럼 / 별도 audit 테이블 / append-only 등)
   - 5년 후 자동 만료/익명화 정책

3. **Launch 시점 vendor 분류 통지 + 이의제기 7일 윈도우**
   - 통지 채널 (이메일/메시지/사이트 알림 중 권고)
   - 통지 카피 draft (정확한 한국어)
   - 7일 윈도우 정책 (윈도우 내 이의제기 = 즉시 정정, 윈도우 후 = 일반 채널)

4. **Model B footer §20① 통신판매중개자 고지 확인**
   - 기존 사이트 footer 의 §20① 고지 grep 결과 보고 (있음/없음)
   - 누락 시 보강 카피 권고

## Acceptance
1. 4 항목 각각 full spec (정책 + 카피 + 워크플로) 본 이슈 코멘트로 보고
2. 후속 implementation 분기 권고 (BE 스키마 / FE 폼 / 운영 admin tool)
3. Legal 자문 형식 (`legal-consult` skill) 준수

## priority
medium. PACAA-XXX FE V1 UI launch 전 본 spec 완료 필요. spec 만 본 child 의 의무 (implementation 은 후속).
