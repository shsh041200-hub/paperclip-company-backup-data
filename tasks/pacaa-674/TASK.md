---
name: "[Security] CF API 토큰 rotation — cfut_iS4HL6rs9... 활성 노출 토큰"
assignee: "ceo"
---

PACAA-658 scrubber 구현 중 발견: [REDACTED-CloudflareUserAPIToken] 가 BE workspace .env 에 현재 활성 상태. 이 토큰은 PACAA-266 이슈 코멘트에 2026-05-01 평문 노출됨. 예정 rotation 2026-05-08 경과.

작업: Cloudflare Dashboard에서 revoke + 새 토큰 발급 + BE .env + PACAA-266 Worker secret 교체.
추가 확인: GitHub webhook secret (1e38fcfe5f38...), Founder Dashboard PW (0kCFM5L...).

DoD: cfut revoke / 새 토큰 BE .env 주입 / Worker secret 교체 / webhook+PW 확인
