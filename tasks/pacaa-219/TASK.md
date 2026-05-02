---
name: "E5 Worker — PAPERCLIP_API_KEY secret 주입 + GitHub PR webhook 통합 검증"
assignee: "backend-engineer"
---

## 배경

[PACAA-190](/PACAA/issues/PACAA-190) (영구 URL `https://paperclip-api.packlinx-api.com`) 완료 후 spin-off. PACAA-167 Phase 2 카나리 가동 직전 마지막 BE 작업.

E5 Worker (`pacaa-e5-pr-webhook`) 의 wrangler.toml docstring (19-32줄) 에 명시된 미완 항목:

```
# Auth: Option B decided — E5 Worker service-account agent
# Agent ID: 6fb76456-5c80-4d8d-bdf8-6325ae2be76d (name: "E5 Worker")
# Board must: POST /api/agents/6fb76456-5c80-4d8d-bdf8-6325ae2be76d/keys {"label":"cloudflare-worker-e5"}
# Then inject the returned key as PAPERCLIP_API_KEY secret below.
```

## 작업

1. CEO/BE 가 보드에게 long-lived agent key 발급 요청 (interaction). 발급은 `feedback_request_confirmation_is_board_only` 룰 따라 보드 전용.
2. 보드 발급된 key 받아서 BE 가 `wrangler secret put PAPERCLIP_API_KEY` 로 Worker 에 주입.
3. GitHub repo (`shsh041200-hub/pkging-platform`) 에 webhook 등록 (Payload URL = E5 Worker 의 workers.dev URL, Secret = WEBHOOK_SECRET).
4. test PR 생성 → E5 Worker 호출 → Paperclip API → CEO/BE wake 확인.

## Acceptance criteria

- 테스트 PR (label `e5-test`) 머지 → Paperclip API 에 GitHub PR event 도달 확인 (활동 로그 1건 이상)
- E5 Worker 가 `https://paperclip-api.packlinx-api.com` 으로 200 응답 받음 (KV 로깅 또는 wrangler tail 로 확인)
- WEBHOOK_SECRET / PAPERCLIP_API_KEY 둘 다 wrangler
