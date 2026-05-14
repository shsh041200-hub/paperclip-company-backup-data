---
name: "[PACAA-674] CF 토큰 sync + Worker 재배포 + webhook/PW rotation"
assignee: "ceo"
---

## 배경
PACAA-674: cfut_iS4HL6rs9... 노출 토큰 보드가 CF Dashboard 에서 revoke 완료 (CEO verify: /user/tokens/verify -> 1000 Invalid). 보드가 adapterConfig.env 에 새 CLOUDFLARE_API_TOKEN 주입.

## 작업 (3개)

### 1. CF 토큰 sync (P0)
- os.environ['CLOUDFLARE_API_TOKEN'] 가 새 토큰인지 verify (curl /user/tokens/verify -> active)
- workspace .env 의 CLOUDFLARE_API_TOKEN=cfut_iS4... (revoked) 줄을 새 값으로 교체 (chmod 0600 유지)
- 또는 deploy.sh 를 os.environ 우선으로 패치

### 2. Worker 재배포 (P0)
- cd workers/e5-pr-webhook && wrangler deploy (PACAA-168)
- cd workers/admin-dashboard && wrangler deploy (PACAA-266)
- 각 deploy log 의 Deployed URL + version ID 코멘트

### 3. Worker 바인딩 secret rotation (P1)
PACAA-266 ccb072a5 같이 노출 가능:
- GitHub webhook secret (1e38fcfe5f38...) — PACAA-168 GITHUB_WEBHOOK_SECRET binding. 새 64-hex 생성 -> wrangler secret put. GitHub repo Settings/Webhooks Secret 갱신 (보드 필요 시 interaction).
- Admin Dashboard PW (0kCFM5L...) — admin-dashboard ADMIN_PASSWORD binding. 새 16+ char -> wrangler secret put. .secrets/admin_dashboard.env sync. 보드에 새 PW interaction 전달 (코멘트 금지).

## DoD
- CF 토큰 verify 새 값 active
- e5-pr-webhook + admin-dashboard 둘 다 신규 deploy 성공
- GITHUB_WEBHOOK_SECRET + ADMIN_PASSWORD wrangler secret put 완료
- Gi
