---
name: "텔레그램 알림 — plan 문서 자동 첨부 + 본문/첨부 더 요약"
assignee: "ceo"
---

## 배경

PACAA-106 클로즈 후 보드 추가 요청 (코멘트 `a5678fb0`, 2026-04-30 05:06 KST):

> 기능을 추가할래 나에게 무언가를 텔레그램으로 보낼때 plan이 포함되는 내용이라면 plan도 문서로써 포함시켜 그리고 내용을 조금더 요약해서 보내 나한테 전체적으로

두 가지 요구:

1. 알림 소스 이슈에 `key=plan` 문서가 있으면 plan 본문을 별도 `.md` 첨부로 함께 발사.
2. 본문/첨부 전반적으로 더 요약 (현재도 합격이지만 좀 더 타이트하게).

## 산출물

### A. plan 자동 첨부

1. `notify-telegram.py` 또는 `_telegram_format.py` 에 `fetch_plan_document(issue_id)` 추가 — `/api/issues/{id}/documents` GET 후 `key=='plan'` 항목의 `body` 반환 (없으면 `None`).
2. 알림 빌드 시 (approval/interaction/review 모두) 소스 이슈에 plan 있으면 두 번째 첨부로 `{IDENTIFIER}_plan_{YYYYMMDD-HHMM}.md` 생성 후 `send_telegram_document` 한 번 더 호출.
3. 본문 "상세" 줄을 변경: plan 있을 때 `상세: ...txt · 플랜: ...md`.
4. plan 첨부 자가검수: 별도 분기 — indent depth 검사/box-divider 차단 OFF (markdown heading/표 허용), 길이 cap 5000자, 비기능 이모지 차단은 유지.

### B. 더 요약

현재 `build_attachment` 의 truncation cap 을 다음으로 좁힘:

- `decision_text`: 200 → 120
- `background`: 300 → 180
- `suggestions`: 항목당 100 → 70, 최대 5개 → 3개
- `risks`: 항목당 100 → 70, 최대 5개 → 3개
- `recent_comments`: 항목당 120 → 80, 최근 3개 → 2개

원문이 새 cap 을 초과하면 `_summarize_for_board` (LLM 요약기) 한 번 통과시켜 cap 안에 들어오게. 단 `--no-summarize` / `--sample` / `--dry-run` 시 LLM 호출 금지 (deterministic 유지).

본문 자체는 지금도 2
