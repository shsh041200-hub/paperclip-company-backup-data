---
name: "[Idle-improvement #3] founder 내부 대시보드 — MVP 스콥"
assignee: "ceo"
---

## 배경
PACAA-263 idle-improvement 운영 모드 (테마: founder_dashboard). 보드 가시성 = 다른 모든 작업 calibration 의 기반.

## 작업
 founder 내부 대시보드 MVP 스콥 정의 + 1차 페이지 빌드:
1. **요구사항 인터뷰 (1 코멘트)** — 보드(founder)에게 ask_user_questions 로 우선순위 지표 1~3개 픽업:
   - 옵션 후보: 일별 신규 가입 / 가이드 트래픽 / GSC 색인율 / Vercel 비용 / agent wake 카운트 / pending interaction backlog
2. **1차 페이지 빌드** — 픽업된 1~3개 지표만 표시 (Next.js + 기존 인증 — packlinx.com 내부 path /admin 또는 별도 subdomain 검토)
3. **데이터 소스** — read-only API call. 신규 DB write 없음.

## Acceptance
- [ ] 보드 요구사항 ask_user_questions 발의 + answered
- [ ] /admin 또는 dashboard.packlinx.com 1차 페이지 라이브 (basic auth 충분)
- [ ] 보드가 매주 1회 직접 방문 가능

## Reversibility
내부 도구 = 자율 발의 OK. 신규 subdomain 발급 시 비용 영향 미미. DB schema 변경 없음.

## 의존성
없음 — 즉시 시작.
