---
name: "[PACAA-905] Google Workspace 전화 인증 한도 재시도 알림"
assignee: "ceo"
recurring: true
---

## 목적

PACAA-905 Google Workspace `packlinx@packlinx.com` 가입 본인 인증 단계에서 `+82 010-2262-1745` 번호가 "인증을 위해 이미 너무 많이 사용한 전화번호" (한국어) 에러로 차단된 상태. Google 의 SMS 인증 한도 reset 기간은 비공개·가변 (24h ~ 수 주 ~ 수 개월). 정기 재시도 알림 + 일정 경과 후 대안 권장.

## 트리거 컨텍스트

- 부모 이슈: PACAA-905
- 차단 시작: 2026-05-19 15:52 KST (스크린샷 timestamp)
- 임시 운영: Cloudflare Email Routing (A 옵션) 로 인박스 forward 중

## 매 fire 실행 단계

1. **본 이슈 PACAA-905 상태 GET** — `status == "done"` 이면 즉시 spawned issue done 처리하고 종료 (이미 보드가 가입 성공해서 close 한 케이스).
2. **PACAA-905 코멘트 전수 GET** — 최신 board 코멘트에 "성공" / "풀렸" / "가입 완료" 키워드 grep. 발견 시 spawned issue 에 "보드 자가 보고 — 성공 확인" 기록 + done.
3. **PACAA-905 의 자기 (CEO) interaction 전수 GET** — `kind=ask_user_questions` 중 prompt 가 "Google 전화 인증 재시도" 로 시작하는 가장 최신 항목 찾기.
4. **간격 판단**:
   - 최신 retry interaction 없으면 → 차단 시작일 (2026-05-19) 이후 경과 일수 계산. ≥ 2일 이면 발의 (Day 2 retry).
   - 최신 retry interaction 있으면 → 그 createdAt 이후 경과 일수 계산. ≥ 7일 이면 발의 (정기 retry). 그 외 silent skip + spawned issue done.
5. **발의 시 stage 판단**:
   - 경과 ≤ 14일: 단순 "오늘 다시 시도해보세요" interaction.
   - 경과 15~59일: "여전히 같은 번호로 막힘. 다른 번호 (가족·지인·KT/SKT 다른 회선) 사용 권장" interaction.
   - 경과 ≥ 60일: "장기 차단. Voice Call 인증 / Google Workspace Sales 직접 영업 / 다른 도메인용 admin email 다른 번호 가입 후 transfer 옵션 보드 결정 필요" interaction.
6. **발의 인터랙션 schema**:
   - kind=ask_user_questions, continuationPolicy=wake_assignee, payload.version=1
   - prompt 시작 = "Google 전화 인증 재시도 (Day N)"
   - questions 1개: 옵션 4개 (성공·풀렸어 / 같은 에러 / 다른 번호 시도해볼래 / 1주일 후 다시 알려줘)
7. **종료**: spawned issue 에 결과 코멘트 (interaction 발의 여부 + Day N + 다음 예상 알림 일자) + status=done.

## 5 가드

1. **Whitelist**: PACAA-905 만 대상. 다른 이슈 mutation 금지.
2. **Rate limit**: 7일 가드. 최근 retry interaction 으로부터 < 7일 이면 silent skip.
3. **Idempotency**: 같은 fire 일자에 같은 prompt prefix 의 interaction 중복 발의 금지 (POST 전 pending GET).
4. **Auto-stop**: PACAA-905 status==done 또는 board "성공" 코멘트 발견 시 본 routine 자체를 PATCH enabled=false 로 정지.
5. **Kill switch**: routine PATCH enabled=false 또는 trigger PATCH enabled=false 즉시 차단.

## 종료 조건

- 보드가 PACAA-905 close → 자동 자체 disable.
- 60일 경과 + 대안 옵션 보드 결정 후 routine 폐기 (별도 child issue 발의 + 본 routine 폐기 PATCH).
