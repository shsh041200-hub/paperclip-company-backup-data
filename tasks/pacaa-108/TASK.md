---
name: "텔레그램 봇 — 샘플 액션 알림 1회 실발사 ([샘플] 마커 필수)"
assignee: "backend-engineer"
---

## 목적

PACAA-107 산출물 (`_telegram_format.py` + `notify-telegram.py --sample=action`) 을 실제 텔레그램 채널에 1회 발사. 보드 모바일에서 결과 확인 → PACAA-106 본격 도입 게이트.

## 보드 사인오프 경로

보드 결정 경로 (a) 채택 — PACAA-106 인터랙션 `abffce29` 응답 (2026-04-30 04:24 KST). PACAA-107 done 유지, 실발사+피드백을 PACAA-106 의 새 보드 승인 게이트로 다시 묶음.

## 안전 조건 (필수)

실제 외부 카드 등록 같은 진짜 액션을 유발하면 안 됨. 샘플임이 한눈에 보이게:

1. 본문 첫 줄을 `[샘플][액션]` 으로 (정상 헤더 `[액션]` 앞에 `[샘플]` 프리픽스).
2. 첨부 본문 첫 줄에 `※ 테스트 발사 — 실제 액션 아님 (PACAA-108)` 한 줄 추가.
3. 본문 마지막에 `※ 응답 불필요 — 모바일 가독성 확인용` 한 줄.

위 마커 추가가 `assert_telegram_safe` 를 깰 가능성:
- `[샘플][액션]` 은 `_HEADER_RE` 의 `^\[(액션|승인|선택|알림)\] ` 와 어긋남 → 헤더 검증을 우회하는 sample-only 예외 추가 필요. 단, 운영 코드에는 절대 흘리지 말 것 (오직 `--sample=action` 경로에서만).
- 25자/줄 폭 — `[샘플][액션] Vercel 결제 카드 등록` 은 13 ASCII + 5 wide(2씩) ≈ 23 visual로 OK. 첨부 마커도 25 한글자 안에서 정리.

## 산출물

1. `_telegram_format.py` — `--sample=action` 경로에 `[샘플]` 마커 추가, 자가검수에 sample-mode 예외 분기. 운영 build_action_body 자체에는 손대지 말 것.
2. 한 번 실발사: `python3 notify-telegram.py --sample=action --really-send` (또는 dry-run 플래그 빼고 발사하는 별도 경로). 발사 후 PACAA-108 에 발사 시각 + 메시지 id (가능하면) + 보드 chat_id 1줄 코멘트.
3. **자가 close 금지.** 보드가 모바일에서 받아 PACAA-106 의 새 `request_confirmation` 에 응답할 때까지 PACAA-108 은 in_progress 유지. 인
