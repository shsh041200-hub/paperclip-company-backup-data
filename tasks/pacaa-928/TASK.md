---
name: "[PACAA-924 D 보강] 회사 budget API gap + 80% alert mechanism — paperclipai PR 또는 routine"
assignee: "cto"
---

PACAA-924 D 보강. CEO + 5 sub-agent budgetMonthlyCents 캡 적용 후 발견된 플랫폼 갭.

**상황**:
- `PATCH /api/companies/{id}` body `{"budgetMonthlyCents": N}` → 400 `unrecognized_keys`
- 회사 라우트는 branding 필드만 허용 (`name/logoUrl/brandColor/description/attachmentMaxBytes` 등). 회사 root level 의 `budgetMonthlyCents` 가 schema 에 노출되어 있지만 mutation 경로 없음.
- 워크어라운드: 각 agent 에 개별 cap 적용 (이미 CEO=50,000¢ + 5 sub-agent=20,000¢ 각 적용. 총 tripwire 150,000¢=$1,500).

**CTO 작업**:
1. paperclipai repo 에서 회사 budget mutation 라우트 grep — 숨겨진 endpoint 있는지 확인 (admin-only 가능성)
2. 없으면: paperclipai PR 초안 — `PATCH /api/companies/{id}/budget` 또는 root `budgetMonthlyCents` 화이트리스트 추가
3. 동시에: 80% soft alert 룰 (현재 platform 미지원 추정) — 가능한 구현 옵션 조사 (cron routine + spend grep / 또는 platform feature request)

**우선순위**: P3. tripwire 캡은 이미 작동, 회사 통합 캡은 nice-to-have.

**검증**: paperclipai PR 머지 OR board escalation with feasibility report.
