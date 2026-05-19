---
name: "이메일 자동 triage / 이슈 발의 파이프라인 (CF Email Worker → CEO)"
assignee: "ceo"
---

## 배경

PACAA-907 의 보드 코멘트 (2026-05-19) — alias 메일을 CEO 가 자율 triage 하길 원함:
> "이메일을 만들면 그 이메일로 오는것들 ceo가 파악해서 처리해야될 문제인지 파악하고 알아서 이슈생성해서 문제 해결"

PACAA-907 의 셋업 (CF Email Routing → founder Gmail forward) 은 닫혔지만, **메일이 CEO heartbeat 까지 도달하는 파이프라인이 없음**. 본 이슈는 그 파이프라인 설계 + 구현.

## 스코프

- alias 3종 (`ceo@` / `alerts@` / `gsc@ `@packlinx-api.com) 수신 메일 → CEO heartbeat 트리거
- CEO 가 LLM triage: junk / 정보성 / actionable
- Actionable: child issue 발의, 자율 액션 (정책 범위 내), 보드 알림
- Junk: 무시 + log
- 정보성: 코멘트 저장만

## 권장 아키텍처 — CF Email Worker (비용 0, ~4~6h)

```
sender → CF Email Routing (packlinx-api.com)
       → forward 1: rpdla041200@gmail.com (사람 백업)
       → forward 2: Email Worker (lambda-like)
            → parse raw email (PostalMime)
            → POST /api/companies/{cid}/issues
                 - title = subject
                 - description = sender + from + body
                 - assigneeAgentId = CEO
                 - status = in_progress
            → CEO wake → triage
```

CF Workers free tier 10만 req/day, 비용 사실상 0. PostalMime 라이브러리 표준. CEO Paperclip API 토큰을 Worker secret 에 주입.

## 대안

- **Gmail API polling**: founder Gmail OAuth + cron. 비번 회수 위험, 자격증명 회수 의무.
- **SendGrid Inbound Parse
