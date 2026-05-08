---
name: "[PACAA-311] notify-telegram.py / _telegram_format.py 보드 보고 포맷 개편 (2026-05-08 directive)"
assignee: "cto"
---

## 배경

보드 directive (PACAA-311, 2026-05-08): Paperclip 봇으로 오는 보고는 (a) 보드 행동이 꼭 필요할 때만 보내고, (b) "현재 X 작업중인데 보드님의 Y 행동이 필요합니다" 형태로, (c) 한국어로, (d) 말줄임(`...` / `…(이하 생략)`) 없이 — 보드가 내용을 모르면 선택·승인 자체가 의미가 없어진다.

승인/선택지 inline 버튼 + 답장 원격 명령 기능은 유지. 변경 대상은 **본문 포맷과 cap, 그리고 send-gate 차단 로직**.

## 변경 범위

파일: `tools/board-visibility/_telegram_format.py`, `notify-telegram.py`

### A. send-gate (필수)

`notify-telegram.py` 의 dispatch 단계에서 `non_actionable` 분류 (in_review 묶음, FYI/observation/status-only) 는 **Telegram 으로 보내지 않는다**. dashboard / 이메일 등 다른 surface 가 노출하더라도 Telegram bot 으로는 차단.

구체적으로 `KIND_NON_ACTIONABLE` 코드 경로는 dry-run 출력만 남기고 Telegram fire 차단. 또는 `--include-non-actionable` 플래그 뒤로만 동작.

### B. 본문 frame opener

모든 A/B/C 클래스 body 가 다음 두 줄로 시작해야 한다:

```
현재 작업: {한 줄}
보드님 필요 행동: {한 줄}
```

그 다음 클래스별 본문. 새 템플릿은 갱신된 packlinx-comms skill 의 "Three classes (templates updated PACAA-311)" 섹션 그대로 구현.

### C. ellipsis 제거 + cap 변경

- `MAX_DOC_CHARS = 1500` → `MAX_DOC_CHARS = 4000`.
- `_truncate` / `…(이하 생략)` 로 끝내는 코드 경로 (line 290, 467, 513, 613 등) **제거**. 대신 4000 자 초과 시 두 가지 중 하나:
  1. 추가 attachment 파일로 split (`{IDENTIFIER}_{kind}_part2_*.txt`).
  2. raise `TelegramFormatViolation` 으로 빌더가 source 를 더
