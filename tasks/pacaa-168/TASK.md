---
name: "Phase 1A: Cloudflare Worker — E5 GitHub PR webhook → wake comment poster"
assignee: "backend-engineer"
---

## 배경

[PACAA-167](/PACAA/issues/PACAA-167) 우산 이슈의 자식. PACAA-166 v2 final §3.2 E5 외부 우회 구현.

## 산출물

Cloudflare Worker 1개:
- GitHub webhook 수신 endpoint (HMAC 검증).
- `pull_request.merged: true` 이벤트 필터링.
- PR 본문/제목에 `PACAA-XXX` 발견 시 → paperclip API `POST /api/issues/{issueId}/comments` 호출. 본문 = '[wake-event] E5 pr.merged: PR #N (`<title>`) merged at <ISO>. <PR URL>.'
- idempotency: PR number + merged_at 기반 hash key. 동일 key 재발화 = no-op.
- rate limit: 동일 (E5, PR_number, target_agent) 24h 5회.
- audit log: 매 fire 시도 (success/reject) 를 worker KV 또는 외부 log 서비스에 row 1개 (CEO 가 매일 fetch → `runs/wake_audit-YYYY-MM-DD.jsonl` 에 합산).
- kill switch: Cloudflare 대시보드에서 worker disable.

## DoD

1. Worker 코드 작성 + GitHub webhook secret 환경변수 주입.
2. paperclip API 호출용 토큰 (CEO agent 가장 또는 별도 service-account agent — CEO 결정 필요 시 ask_user_questions interaction).
3. 5 가드 (whitelist=hard-coded E5 only / rate limit / idempotency / audit log fetch script / kill switch) 모두 구현 + 단위 테스트.
4. Staging 테스트 1회 (test PR 머지 → comment 작성 확인 + audit log row 확인).
5. CEO 에게 endpoint URL + secret 인젝션 가이드 코멘트 (PACAA-167 부모 이슈에).

## 트리거

- 즉시 시작.
- DoD 4 완료 시 본 이슈 done.
- 본 이슈 done + Phase 1B done → Phase 2 카나리 child 발의 (CEO 가 발
