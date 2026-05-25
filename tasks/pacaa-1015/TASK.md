---
name: "[PACAA-905] Google Workspace 전화 인증 한도 재시도 알림"
assignee: "ceo"
---

## 목적

PACAA-905 Google Workspace `packlinx@packlinx.com` 가입 본인 인증 단계에서 `+82 010-2262-1745` 번호가 "인증을 위해 이미 너무 많이 사용한 전화번호" (한국어) 에러로 차단된 상태. Google 의 SMS 인증 한도 reset 기간은 비공개·가변 (24h \~ 수 주 \~ 수 개월). 정기 재시도 알림 + 일정 경과 후 대안 권장.

## 트리거 컨텍스트

* 부모 이슈: PACAA-905
* 차단 시작: 2026-05-19 15:52 KST (스크린샷 timestamp)
* 임시 운영: Cloudflare Email Routing (A 옵션) 로 인박스 forward 중

## 매 fire 실행 단계

1. **본 이슈 PACAA-905 상태 GET** — `status == "done"` 이면 즉시 spawned issue done 처리하고 종료 (이미 보드가 가입 성공해서 close 한 케이스).
2. **PACAA-905 코멘트 전수 GET** — 최신 board 코멘트에 "성공" / "풀렸" / "가입 완료" 키워드 grep. 발견 시 spawned issue 에 "보드 자가 보고 — 성공 확인" 기록 + done.
3. **PACAA-905 의 자기 (CEO) interaction 전수 GET** — `kind=ask_user_questions` 중 prompt 가 "Google 전화 인증 재시도" 로 시작하는 가장 최신 항목 찾기.
4. **간격 판단**:
   * 최신 retry interaction 없으면 → 차단 시작일 (2026-05-19) 이후 경과 일수 계산. ≥ 2일 이면 발의 (Day 2 retry).
   * 최신 retry interaction 있으면 → 그 createdAt 이후 경과 일수 계산. ≥ 7일 이면 발의 (정기 retry). 그 외 silent skip + spawned issue done.
5. **발의 시 stage 판단**:
   * 경과 ≤ 14일: 단순 "오늘 다시 시도해보세요" interaction.
   * 경과 15\~59일: "여전히 같은 번호로 막힘. 다른 번호 (가족·지인·KT/SKT 다른 회선) 사용 권장" interaction.
   * 경과 ≥ 60일: "장기 차단. Voice Call 인증 / Google Workspace Sales 직접 영업 / 다른 도메인용 admin
