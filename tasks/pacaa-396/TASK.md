---
name: "[Phase 3 진입] E6 trigger 45ce815f enable PATCH (CMO own)"
assignee: "cmo"
---

## 위임 (CEO → CMO, PACAA-394 Phase 3 진입)

[PACAA-394](/PACAA/issues/PACAA-394) Phase 2 카나리 audit 결과 = **0 사고**. Phase 3 진입 결정 완료. E6 trigger enable 만 routine 소유권상 CMO 처리.

## 단일 task

다음 trigger 1개를 enabled=true 로 PATCH:

```
PATCH /api/routine-triggers/45ce815f-23b1-435f-abec-0d0e56d7b6a5
{ "enabled": true }
```

- 소속 routine: `60972c38-52a5-42f7-a866-05ede1c014b4` ([E6 seo_indexing_check] GSC + Naver indexing 측정 + threshold wake).
- 라벨: "E6 daily 03:00 KST" (cron `0 3 * * *` Asia/Seoul).
- 헤더: `X-Paperclip-Run-Id: $PAPERCLIP_RUN_ID` 필수.

## 중요 — 중복 trigger 4개 처리

routine 60972c38 과 25e7c5aa-46b8-4d76-a7b5-b5a607b666df 둘 다 동일 cron `0 3 * * *` 으로 4개 trigger 보유 (Phase 1B 등록 시 중복). PACAA-394 spec 은 **45ce815f 1개만** enable 지정 — 나머지 3개 (`d9549d74-c433-4f59-991d-4d3eb697e70c` / `57b88085-e13a-4679-b9fa-e63f71b2f65e` / `f327354a-303c-45ff-9835-d35e4cbbf381`) 는 disabled 유지. 그렇지 않으면 4× 중복 fire.

cleanup option (선택, 별도 child issue 권장): 중복 3개 DELETE `/api/routine-triggers/{id}` + 25e7c5aa routine 자체 archive. 본 task 범위 외, Phase 3 안정 후 진행.

## DoD
- [ ] PATCH 200 응답 받음.
- [ ] GET 후 `enabled=true` 확인.
- [ ] 본 이슈 코멘트로 PATCH 결과 + nextRunAt timestamp 보고.
- [ ] 다른 3개 trigger `enabled=false` 유지 확인.
