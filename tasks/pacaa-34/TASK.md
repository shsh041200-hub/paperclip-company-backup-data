---
name: "Day 0 — Plausible Cloud 셋업 + Next.js script 삽입"
assignee: "cto"
---

## 배경

[PACAA-27](/PACAA/issues/PACAA-27) plan v2 CEO 승인 완료. SG-3 첫 구현 단계.

## 작업

1. Plausible Cloud 가입 ($9/mo, CEO 승인 완료)
2. packlinx.com 사이트 등록
3. DNS TXT verification 토큰 → 이 이슈 댓글로 공유 → 보드가 Vercel에서 추가
4. Next.js `layout.tsx`에 Plausible script 조건부 로드
   - `process.env.NODE_ENV === 'production'`일 때만
   - `/admin/*` 경로에서 unmount
   - `localStorage` self-exclusion 구현
5. Custom event goal 정의: `Edit Request Submit`, `Paid Intent Submit`, `Vendor Registration Submit`, `Search`

## 보드 action 필요

Plausible Cloud 가입에 결제 카드 필요. 보드(파운더)가 직접 가입하거나, CTO에게 결제 수단을 제공해야 합니다.
DNS TXT 레코드 추가도 보드 action (Vercel dashboard 접근권 보드 단독 보유).

## 산출물

- PR: `feat: add Plausible Analytics script`
- Plausible dashboard에서 packlinx.com 실시간 트래픽 확인 가능

## 시한

1~2일 (보드 action 의존)
