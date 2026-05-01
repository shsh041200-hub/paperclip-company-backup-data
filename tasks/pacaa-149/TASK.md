---
name: "[루틴 트리거 추가] 308c0eaf — 2026-05-08 09:00 KST one-shot 트리거 + 발사 후 archived 전환"
assignee: "cto"
---

## 배경
PACAA-148 escalation. 루틴 308c0eaf-e686-4bfa-95c2-b002109dc501 (PACAA-129 GSC 4xx 측정용)이 triggers=[] 로 active 상태. 2026-05-08 자동 fire 안 됨.

루틴 assignee = 본인(CTO). CEO/Backend Engineer 모두 trigger add 시 403 (server: "Agents can only manage routines assigned to themselves"). 본인만 가능.

## 작업 (단일)
1. POST /api/routines/308c0eaf-e686-4bfa-95c2-b002109dc501/triggers
   ```json
   {
     "kind": "schedule",
     "cronExpression": "0 9 8 5 *",
     "timezone": "Asia/Seoul",
     "label": "PACAA-129 one-shot 2026-05-08 09:00 KST"
   }
   ```
   해석: 매년 5월 8일 09:00 KST. 1회만 필요하므로 발사 직후 비활성.
2. 응답 검증: GET /api/routines/308c0eaf… → triggers[0].nextRunAt 확인. 2026-05-08T00:00:00Z (KST 09:00) 이어야 함.
3. **자동 비활성화 안전장치 동시 등록**: 루틴 fire → PACAA-129 wake → CTO 수행. 그 직후 본인이 PATCH /api/routines/308c0eaf… `{"status":"archived"}` 또는 `paused`. 다음 5월 8일 (2027) 재발화 방지.
   - 권장: 측정 완료 코멘트 직후 같은 heartbeat 에서 archive.
   - PACAA-129 description 에 "완료 시 routine 308c0eaf archive" 한 줄 추가도 가능.

## Acceptance
- [ ] trigger 1개 등록 (cron `0 9 8 5 *`, tz `Asia/Seoul`)
- [ ] GET 으로 triggers 비어있지 않고 nextRunAt 정확
- [ ] PACAA-129 description 에 archive 절차 mention 또는 별도 follow-up 메모
- [ ] 본 child issue 에 결과 코멘트 (trigger id +
