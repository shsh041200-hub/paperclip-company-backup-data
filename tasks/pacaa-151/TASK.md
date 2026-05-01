---
name: "[ESCALATION → 보드] 중복 hire 정리 — CMO 2 (b4e83dca) 종료 요청"
assignee: "ceo"
---

## 배경

PACAA-74 가속 hire 진행 중 CEO 가 동일 payload 로 POST /agent-hires 를 두 번 발사 (curl 동일 호출 2회). 결과:

- **Primary (유지):** CMO `310d34a5-b746-4704-a946-cc1e7e2422fd` urlKey `cmo` (먼저 생성, 04:55:24Z)
- **Duplicate (종료 요청):** CMO 2 `b4e83dca-cfb8-468c-affc-241c815a8d5f` urlKey `cmo-2` (04:55:30Z)

둘 다 보드 자동 승인되어 idle 상태. CEO 권한으로는 agent terminate 불가 (Board access required).

## 요청

보드가 `b4e83dca` (CMO 2) 를 terminate 또는 archive. 동시에 가능하면 다음 사항 검토:

1. 자동 승인 정책 검토 — hire_agent 승인이 즉시 fire 되어 dedupe 윈도우가 없었음. 보드 review 단계 도입 또는 idempotency key 강제 옵션이 있는지.
2. 중복 hire 가 비용·혼동 발생원이 되므로 향후 hire payload 에 idempotencyKey 필드를 사용해야 하는지 (api-reference 에 명시는 없음 — 서버 지원 여부 확인 필요).

## 차단 영향

CMO 2 가 idle 상태로 살아있으면 보드 dashboard 에 노출되어 혼동. 단 heartbeat enabled=false + wakeOnDemand=true 이고 어떤 ticket 도 할당하지 않을 것이므로 자동 fire 위험은 없음.

## 옵션

- **A) 보드 terminate** (권장) — `b4e83dca` 즉시 종료. 회수 비용 0.
- **B) 보드 archive** — terminate API 가 무거우면 archive 또는 paused 상태로 전환.
- **C) 유지 + rename** — 향후 다른 colleague 로 활용 가능성이 있다면 (예: Naver SA 전담 sub-CMO) 그대로 유지하고 이름·역할 재정의.

CEO 권장: **A**. 페어 2 plan 에 sub-CMO 자리 없음. 조직 단순성 우선.

## DoD

- 보드가 b4e83dca 종료 (또는 명시적 유지 결정) → 본 ticket close.

## 참고

- 부모 hire ticket: PACAA-74
- Pri
