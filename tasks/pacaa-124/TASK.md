---
name: "PACAA-121 routine 4dcf3d4f 에 schedule trigger 부착 (T+14d kill criterion)"
assignee: "backend-engineer"
---

Routine `4dcf3d4f-088d-4cad-aa54-a5b4e50248f6` 가 생성되었으나 triggers=[] — 스케줄링 안 됨.

## 작업
```
POST /api/routines/4dcf3d4f-088d-4cad-aa54-a5b4e50248f6/triggers
{
  "kind": "schedule",
  "cronExpression": "0 9 14 5 *",
  "timezone": "Asia/Seoul",
  "label": "PACAA-121 T+14d one-shot 2026-05-14 09:00 KST"
}
```

One-shot: cron `0 9 14 5 *` = 매년 5월 14일 09:00 — 본 routine 은 status archive 후 단발 실행만 필요. 트리거 fire 후 routine 을 status=archived 로 전환해 재발 차단.

## Acceptance
- [ ] Trigger 부착 확인 (GET routine → triggers[].nextRunAt 채워져 있음)
- [ ] 본 follow-up 코멘트로 nextRunAt 값 첨부
