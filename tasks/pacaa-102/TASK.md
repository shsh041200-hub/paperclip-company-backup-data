---
name: "[Setup] Monday 09:30 KST weekly self-audit routine 생성"
assignee: "legal-counsel"
---

## 목적

Legal Counsel 본인의 주간 자가 점검 routine 을 생성한다 (PACAA-101 §1.5). CEO 가 대신 만들 수 없음 — Paperclip 권한 모델: agents can only manage routines assigned to themselves.

## 작업

`POST /api/companies/{companyId}/routines` 로 routine 생성:
- title: `Legal Counsel — Weekly self-audit`
- assigneeAgentId: 본인 (`54623669-64c6-402d-b87b-c0b8ebae3940`)
- projectId: `f0cad884-57d7-4a3e-b1bb-fa93a4fc0b2c` (packlinx website)
- goalId: `2757be4c-f2fe-44a2-a686-edd7e576f178` (Vision root)
- priority: medium
- concurrencyPolicy: `skip_if_active`
- catchUpPolicy: `skip_missed`

이어서 schedule trigger 추가:
- kind: `schedule`
- cronExpression: `30 9 * * 1` (월요일 09:30 KST)
- timezone: `Asia/Seoul`
- label: `Monday 09:30 KST weekly self-audit`

## 점검 항목 (routine 이 fire 시 작업)

1. 지난 7일간 SG-1~4 활동 issue 스캔 (PACAA, label/parent/goal 기반)
2. 각 활동에서 새로운 법적 surface 발생 여부 확인 — Legal Counsel 호출 누락 케이스 식별
3. 누락 발견 시 회고적 자문 발행 (호출 issue 코멘트 + 호출자 @mention)
4. Goal 트리 빈 구멍 (어느 SG / 어떤 빈 구멍) 검사 — 발견 시 본 routine fire 의 자식 issue 로 보드 보고
5. 0-fire 일에도 1줄 로그 ("이번 주 N개 SG 활동 검토 완료, 빈 구멍 0건")

## 디스클레이머

자문은 참고용. 외부 변호사 자문 미도입 (보드 책임 부담).

## 완료 시

routine ID 를 본 issue 코멘트로 보고하고 status `done`. 첫 fire = 다음 월요일 09:30 KST.

## Reference

p
