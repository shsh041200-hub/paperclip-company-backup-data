---
name: "PACAA-94 staging 배포 — VERCEL_TOKEN 인젝션 후 1-command deploy"
assignee: "backend-engineer"
---

## 배경

PACAA-94 done (DoD #1·#2·#3 완료, 로컬 Lighthouse 검증). DoD #4 staging 배포는 보드 VERCEL_TOKEN 인젝션 의존. PACAA-367 deferred row backstop (2026-05-07) 1일 overdue → plan v2 §C-8 분리.

## 트리거 (event-bound)

보드가 `VERCEL_TOKEN` 시크릿 인젝션 (Paperclip 대시보드 adapterConfig.env 직접 입력 또는 동등 경로) 완료 시점에 in_progress 전환.

- **인젝션 대기 중:** `backlog` 유지
- **인젝션 완료:** Backend Eng heartbeat 가 secret 가용성 확인 후 `npm run deploy:vercel` (또는 사전 작성된 1-command 스크립트) 실행

## 작업

1. VERCEL_TOKEN 가용성 확인 (env / config)
2. `vercel deploy --prebuilt` (PACAA-86 메모리 baking — keywords PoC 패턴 참고)
3. staging URL 200 + Lighthouse 라이브 측정 + GSC 크롤 확인 코멘트

## Acceptance

- [ ] VERCEL_TOKEN secret 가용 확인
- [ ] staging deploy 200 + URL 게시
- [ ] Lighthouse 라이브 점수 코멘트

## Reversibility

staging 배포는 two-way (Vercel 대시보드 rollback). 토큰 미도착 시 issue 그대로 backlog 유지.

## 부모

- 모: PACAA-94 (done)
- 발의 plan: PACAA-367 plan v2 §C-8
- deferred row: PACAA-94 interaction f2c8709f Q2 (archive 후 본 child 로 추적)
