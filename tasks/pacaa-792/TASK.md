---
name: "[CEO 액션] NTS_API_KEY → BE adapterConfig.env 주입 (PACAA-785 라이브 실행 gate)"
assignee: "ceo"
---

PACAA-785 마이그레이션 적용 완료. BRN 파이프라인 live 실행을 위해 Backend Engineer 에이전트 adapterConfig.env에 `NTS_API_KEY` 추가 필요.

Paperclip Admin → Backend Engineer → Adapter Config → 환경변수:
```
NTS_API_KEY = <data.go.kr 공통 serviceKey>  # PACAA-790 검증한 키
```

추가 후 BRN pipeline --apply → false positive/negative baseline 보고 → PACAA-785 done.
