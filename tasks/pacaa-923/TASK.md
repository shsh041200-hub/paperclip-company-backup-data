---
name: "[PACAA-921 P1·P2 CEO-self] heartbeat 재튜닝 + Phase 5 quick-exit + backup-*.md 분리"
assignee: "ceo"
---

PACAA-921 board accept 의 **CEO 자체 처리** 묶음.

## E. CEO heartbeat 재튜닝 (P1)
- `intervalSec` 300 → 900 (PACAA-828 Sole-broker 응답 절충 sibling 권장값)
- `maxTurnsPerRun` 3000 → 500
- `maxAttempts` 10 → 3
- `maxConcurrentRuns` 10 → 3
- `wakeOnDemand` true 유지
PATCH /api/agents/{ceo} runtimeConfig.heartbeat + maxTurnsPerRun + maxAttempts + maxConcurrentRuns.

## F. HEARTBEAT.md Phase 5 quick-exit path (P1)
- 'idle wake obligation / Phase 5 강제 회전' 룰 재작성 — quick-exit path 허용 (200 토큰 이내 종료 조건 명시).
- AGENTS.md or HEARTBEAT.md 편집.
- PACAA-237 root-cause guardrail 의 본질 유지 (vacuous no-op 만 차단, 진짜 idle 은 200t 종료 OK).

## G. backup-2026-05-07*.md → backups/ 디렉토리 분리 (P2)
- `$AGENT_HOME/backup-work/paperclip-company-backup-data/agents/*/*.backup-2026-05-07` 파일을 `backups/` 별도 디렉토리로 이동.
- 다음 backup 푸시 시 instructions 트리에서 제외.

## 검증
- E: GET /api/agents/{ceo} → new values 반영.
- F: HEARTBEAT.md diff + 다음 idle wake 가 quick-exit 사용 (Journal 라인 카운트 감소).
- G: GitHub backup repo 의 agents/*/*.backup-* 0건.
