---
name: "fix(emails): FROM_ADDRESS env-driven for Path A deploy"
assignee: "backend-engineer"
---

## 목적

[PACAA-391](/PACAA/issues/PACAA-391) Path A (Resend 도메인 인증 없이 빠른 배포) 위해 `FROM_ADDRESS` 를 env-driven 으로 1-line 변경. 보드 Path A 선택 (CEO 17:03 응답).

## 변경 사항 (1 line, branch `feat/quote-form-plausible-PACAA-358`)

`lib/emails/index.ts:7`

```diff
-export const FROM_ADDRESS = 'noreply@packlinx.com';
+export const FROM_ADDRESS = process.env.RESEND_FROM_ADDRESS ?? 'onboarding@resend.dev';
```

**Why:** 현재 `noreply@packlinx.com` 하드코딩. Resend 는 발신 도메인 미인증 시 발송 차단. `onboarding@resend.dev` 는 Resend 가 모든 가입자에게 즉시 발송 허용하는 기본 발신자 (CTO 2026-05-08T22:38 advisory). default 를 `onboarding@resend.dev` 로 두면 보드 Vercel env 등록 부담 3개 → 그대로 유지 (4번째 env 추가 없음). 향후 `packlinx.com` 도메인 인증 완료 시 Vercel env `RESEND_FROM_ADDRESS=noreply@packlinx.com` 한 줄 추가로 production 발신자 복원.

## 행동 (Backend Engineer)

1. branch `feat/quote-form-plausible-PACAA-358` checkout (PR #27 head)
2. `lib/emails/index.ts:7` 1-line 변경
3. 커밋 메시지: `fix(emails): FROM_ADDRESS env-driven for Path A deploy (PACAA-410)`
4. push → PR #27 자동 갱신
5. 본 issue 코멘트로 commit SHA 보고 + status=done

## 완료 기준 (DoD)

- [ ] `lib/emails/index.ts:7` env-driven 패치 푸시
- [ ] PR #27 head 에 신규 commit 반영 (CI green)
- [ ] 본 이슈 commit SHA 보고
