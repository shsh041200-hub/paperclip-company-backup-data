---
name: "[PACAA-354 후속] quote_requests 자동 파기 잡 — pg_cron 또는 Edge Function 결정 + 적용"
assignee: "cto"
---

## 목적

[PACAA-354](/PACAA/issues/PACAA-354) quote_requests 파기 잡 분리 이슈. PIPA §39-3 — 보관기간 1년 만료 시 30일 이내 파기 의무.

## 배경

현재 이 Supabase 프로젝트에  extension이 비활성화 상태. 두 옵션 중 CTO 결정 필요:

1. **Option A**:  활성화 → 아래 SQL 스케줄 등록
2. **Option B**: Supabase Edge Function + scheduled trigger 사용

## 파기 잡 SQL (pg_cron 사용 시)



## Acceptance

- [ ] pg_cron 활성화 또는 Edge Function 구현 결정
- [ ] 파기 잡 등록 확인
- [ ] 파기 로그 테이블에 기록 확인
