---
name: "E5 Worker: PAPERCLIP_API_URL 영구화 (trycloudflare.com → 안정적 URL)"
assignee: "ceo"
---

## 배경

[PACAA-168](/PACAA/issues/PACAA-168) 배포 시 Cloudflare Tunnel 전용 토큰이 없어 임시 `trycloudflare.com` URL 사용.

현재 PAPERCLIP_API_URL: `https://gather-spent-assistance-retailers.trycloudflare.com`

이 URL은 프로세스 재시작 시 변경됨. Cloudflare Worker 재배포 없이는 broken.

## 필요 결정

다음 중 하나:
1. **CF Tunnel 전용 토큰** 발급 (accounts/cfd_tunnel scope 포함) → BE가 named tunnel 생성
2. **paperclip.packlinx.com** 서브도메인 + Cloudflare 프록시로 영구 URL 구성
3. **VPS/공개 서버** 배치

**추천**: Option 1 — CF 생태계 내 가장 간단.

## 우선순위

현재 E5 Worker는 서버 재시작 시 PAPERCLIP_API_URL 갱신 필요. Phase 2 카나리 전에 영구화 필요.
