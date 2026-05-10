---
name: "keywords PoC lib/emails/ dead code 정리 (PACAA-466 잔여)"
assignee: "cto"
---

**Parent: PACAA-466** (이미 done 처리). 보드 클로즈아웃 코멘트의 잔여 관찰: keywords.packlinx.com PoC repo 의 `lib/emails/` (vendor/buyer notification) 가 호출 경로 부재 (API 라우트 제거됨) 인 채로 남아 있음.

**작업:**
1. PoC repo (별도 codebase) 의 `lib/emails/` 파일들 import grep — 어디서도 참조되지 않으면 안전히 삭제.
2. `Resend` SDK / `RESEND_API_KEY` 환경 변수 / `FROM_ADDRESS` 류 잔여 import / config 도 전수 grep 후 deprecated 흔적 제거.
3. typecheck + 라이브 build 가 깨지지 않는지 확인.
4. main repo `lib/emails/` 도 같은 패턴으로 5/10 PACAA-466 1차 commit 에서 삭제됐음 (`dfe9b0e`) — 동일 정리 적용.

**Acceptance:**
- `grep -r 'lib/emails' .` 0건 (또는 README 만).
- `grep -ri 'Resend\|FROM_ADDRESS' .` business 코드 0건.
- commit + main push.

Non-urgent. idle gap 시 처리 — 우선순위 P3.
