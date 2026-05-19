---
name: "이메일 triage Worker 배포 — API 토큰 발급 + CF Routing 추가 (CEO 액션)"
assignee: "ceo"
---

## 배경
[PACAA-910](/PACAA/issues/PACAA-910) Worker 코드 완성. 배포를 위해 CEO 액션 4단계 필요.

## 체크리스트

### 1. Email Worker 서비스 계정 에이전트 생성

e5-pr-webhook 패턴과 동일하게 별도 서비스 에이전트 생성:
- name: `Email Worker`
- 기능: issue POST/PATCH 전용 (human-like heartbeat 불필요)

### 2. API Key 발급

```
POST /api/agents/{new-agent-id}/keys
{"label": "cf-email-worker"}
```

반환된 key를 메모.

### 3. Worker 배포

```bash
cd /home/rlatjsgur/.paperclip/instances/default/workspaces/3177894b-a1ee-4d88-8aa1-ba902b01f141/workers/email-triage
npm install
wrangler secret put PAPERCLIP_API_KEY   # 2에서 발급한 key
wrangler deploy
```

### 4. CF Email Routing 추가 (packlinx-api.com zone)

Cloudflare dashboard → Email Routing → Routes

각 alias에 Worker fork 추가:
- `ceo@packlinx-api.com` → Gmail forward (기존 유지) + Send to Worker `packlinx-email-triage`
- `alerts@packlinx-api.com` → Gmail forward (기존 유지) + Send to Worker `packlinx-email-triage`
- `gsc@packlinx-api.com` → Gmail forward (기존 유지) + Send to Worker `packlinx-email-triage`

### 5. 수락 테스트

`ceo@packlinx-api.com` 으로 테스트 메일 발송 → 1분 내 PACAA-### 이슈 자동 생성 확인.

## 완료 기준

- Worker 배포 상태 active
- 테스트 메일 → 이슈 자동 생성 확인
- Gmail forward 계속 동작
- [PACAA-911](/PACAA/issues/PACAA-911) 블로커 해제
