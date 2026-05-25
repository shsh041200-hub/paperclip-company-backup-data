---
name: "[CEO] Stale Sweep Telegram 봇 토큰 복구 — 주간 sweep 전송 실패 (PACAA-1010)"
assignee: "ceo"
---

**문제:** 2026-05-25 09:00 KST PACAA-1010 주간 sweep fire 시 Telegram sendMessage 불가.

- `$AGENT_HOME/config/telegram-stale-sweep.json` 파일이 워크스페이스에 없음.
- 워크스페이스/회사 디렉토리에서 발견된 봇 토큰 3개 모두 `getMe` → 401 Unauthorized.
- Telegram 자체는 reachable, 토큰 revoke 사유 추정.

**영향:** PACAA-54 hub spec 의 primary delivery surface (`@Stale_Blocked_Issue_Sweep_bot`) 단절. 본 fire 는 PACAA-1010 코멘트 fallback 만 전달.

**필요 조치 (보드):** BotFather 에서 토큰 재발급 → CEO 에게 Paperclip0412_bot 으로 전달. CEO 가 `config/telegram-stale-sweep.json` 재생성 (chmod 600). 다음 fire 2026-06-01 09:00 KST 전까지 복구 필요. 동일 채널 이유로 Daily Digest 봇도 함께 점검 필요.
