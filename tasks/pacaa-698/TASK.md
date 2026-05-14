---
name: "Anthropic Agent SDK $200 크레딧 — 6/15 redeem + 사용량 모니터링"
assignee: "ceo"
---

PACAA-697 후속. 6/15부터 Max 20x plan 의 Agent SDK 사용분이 별도 $200/월 크레딧 풀로 분리됨.

## 트리거

* Anthropic 으로부터 redeem 알림 이메일 수신 시 (6월 중)
* 보드가 redeem 클릭 후 본 ticket wake

## Acceptance

1. 6월 redeem 클릭 완료 (보드)
2. 첫 30일 agent 토큰 사용량 vs $200 캘리브레이션 보고
3. extra usage 토글 정책 결정 (default OFF — 한도 초과 시 fleet stall 수용 vs 켜둘지)
4. fleet stall 알림 보강 필요 시 CTO child issue 발의

## 관련

* PACAA-697 원본 이메일
