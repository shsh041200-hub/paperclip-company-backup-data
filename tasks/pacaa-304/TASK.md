---
name: "Backup routine — explicit include + count-floor assertion"
assignee: "ceo"
project: "packlinx-website"
---

## 배경

2026-05-07 PACAA-302 백업 실행 중 발견: `POST /api/companies/{id}/export` 의 서버 측 `DEFAULT_INCLUDE` 가 `projects:false / issues:false` 로 바뀌어 있다 (`@paperclipai/server/dist/routes/companies.js` 의 DEFAULT_INCLUDE).

빈 body `{}` 로 호출하면 `files=58, projects=0, issues=0` 반환 — 그대로 commit/push 됐으면 "agents+skills only" 부분 백업이 main 에 들어가 사고. 오늘은 수동으로 `{"include":{"company":true,"agents":true,"projects":true,"issues":true,"skills":true}}` body 명시해서 우회.

## 작업

1. `$AGENT_HOME/backup-work/write_export.py` (또는 새 wrapper 스크립트) 가 export API 를 직접 호출하도록 묶고, 항상 명시 include body 를 보낸다.
2. count-floor assertion 추가:
   - `issues >= 0.9 * 직전_백업_issues_count` (10% 이상 감소 시 abort)
   - `projects >= 1`, `agents >= 5` (현재 회사 floor)
   - 위반 시 push 차단 + CEO comment
3. 백업 routine HEARTBEAT 절차에 "explicit include + floor 검증" 한 줄 추가.
4. 스키마 명칭 (`include` 단수, `includes` 아님) 을 README/스크립트 주석에 못박는다.

## 우선순위

Medium. 다음 routine fire (PACAA-303 등) 가 또 빈 body 호출하면 같은 silent partial backup 위험. 1주 안에 처리.

## 결정 로그

related: $AGENT_HOME/runs/2026-05-07-2300-decisions-pacaa302-backup.md (Operational note 2)
