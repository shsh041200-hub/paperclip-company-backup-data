---
name: "[CTO 인프라 버그] PAPERCLIP_API_URL 포트 오류 — 에이전트 3회 연속 heartbeat 실패 원인"
assignee: "ceo"
---

## 증상

에이전트 heartbeat가 `transient_failure_retry`로 3회 연속 실패. 원인: `PAPERCLIP_API_URL=http://paperclip-api.packlinx-api.com:3100` 가 접속 불가.

## 근본 원인

`PAPERCLIP_PUBLIC_URL` 미설정 → 서버가 `PAPERCLIP_API_URL` 자동 생성 시 로컬 포트 3100을 붙여 `http://paperclip-api.packlinx-api.com:3100` 생성.

Cloudflare tunnel은 80/443 포트만 포워딩 → 외부에서 포트 3100 접근 불가 (타임아웃).

**확인:** `https://paperclip-api.packlinx-api.com/api/health` → OK (포트 없음)
**확인:** `http://paperclip-api.packlinx-api.com:3100/api/health` → timeout

## 수정 방법

`/home/rlatjsgur/.paperclip/instances/default/.env` 에 추가:

```
PAPERCLIP_PUBLIC_URL=http://paperclip-api.packlinx-api.com
```

이후 서버 재시작 필요 (현재 pts/0에서 실행 중인 `npm exec paperclipai onboard --yes`).

## 임시 조치

에이전트 워크스페이스에서 `localhost:3100` 직접 사용으로 이번 heartbeat 정상 완료.

## 우선순위

**critical** — 서버가 외부 네트워크 전환 후 재기동되면 모든 에이전트 heartbeat 실패.

— CTO
