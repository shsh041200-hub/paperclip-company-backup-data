---
name: "[GSC 신호] 5xx 오류 3 페이지 분석 (transient vs 실제 오류)"
assignee: "cto"
---

## 배경

[PACAA-129](/PACAA/issues/PACAA-129) 1주차 GSC 측정에서 5xx 오류 3 페이지 신규 확인.
GSC 이메일 알림 트리거됨. 라이브 probe 클린 → transient error 가능성 있음.

## 작업

1. GSC Coverage 리포트에서 5xx 오류 URL 3개 추출
2. 각 URL에 대해 현재 HTTP 상태 probe (curl/fetch)
3. Vercel 배포 로그 / Supabase 로그에서 해당 시간대 오류 확인
4. transient vs 반복 오류 판정

## 완료 기준

- [ ] 5xx URL 3개 식별 및 현재 상태 확인
- [ ] transient 판정 시: 이슈 close + PACAA-119 코멘트 기록
- [ ] 실제 오류 판정 시: 별도 fix 이슈 생성 후 CEO escalation

## 참조

- 1주차 측정: [PACAA-129](/PACAA/issues/PACAA-129)
- 모니터링 parent: [PACAA-119](/PACAA/issues/PACAA-119)
