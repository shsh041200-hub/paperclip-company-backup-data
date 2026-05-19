---
name: "이메일 자동 triage — CF Email Worker 구현 (PACAA-909 자식)"
assignee: "cto"
---

## 배경
[PACAA-909](/PACAA/issues/PACAA-909) 보드 결정 옵션 A (Read-only triage) 확정. 이메일 → CEO heartbeat 파이프라인의 Worker 부분 구현.

## 스코프
1. CF Email Routing 추가 라우팅: 3 alias (`ceo@`/`alerts@`/`gsc@` @packlinx-api.com) 를 기존 founder Gmail forward 외에 Email Worker 로도 fork (Catch-all 또는 alias 별).
2. Cloudflare Worker 코드:
   - PostalMime 로 raw email parse
   - POST `/api/companies/d5e183da-c58f-4124-8075-493330dce4c4/issues`
     - `title` = `[email:{alias}] {subject[:80]}`
     - `description` = `From: {from}
To: {to}
Subject: {subject}
DKIM: {pass|fail}

{body_text[:2500]}`
     - `assigneeAgentId` = `e33ecade-45dc-47ea-9d46-78ef72e8831c` (CEO)
     - `status` = `in_progress`
     - `priority` = `medium`
     - `labels` = `["email-inbound","email:{alias}"]`
   - body > 2.5KB → 후속 PATCH 로 full body 첨부
3. Worker secret 주입: 신규 Paperclip API token (CEO 토큰과 분리, scope 좁힘 — issue POST/PATCH 만). CEO 가 보드 dashboard 통해 발급 후 Worker secret 으로 등록.
4. UA 헤더: `paperclipai-email-worker/1.0` 명시 (CF 1010 회피).

## Acceptance
- `ceo@packlinx-api.com` 으로 테스트 메일 송신 → 1분 내 신규 PACAA-### 이슈 자동 생성
- title 에 `[email:ceo]` prefix, description 에 from/subject/DKIM/body 포함
- CEO heartbeat 가 새 이슈에 wake (`issue_assigned`)
- found
