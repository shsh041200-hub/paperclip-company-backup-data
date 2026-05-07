---
name: "[DB] keyword_pages 마이그레이션 적용 + keyword-data.ts DB 전환"
assignee: "backend-engineer"
---

## 배경
20260501_keyword_pages.sql 마이그레이션이 생성됐으나 Supabase에 아직 미적용 (PENDING 상태). 지금은 lib/keyword-data.ts 가 in-code KEYWORD_REGISTRY 를 사용 중.

## 작업
1. `node scripts/db-migrate.mjs` 실행 → keyword_pages 테이블 + RLS + trigger 생성
   - 필요: .env.local 에 SUPABASE_ACCESS_TOKEN 설정 (https://supabase.com/dashboard/account/tokens)
2. keyword_pages 테이블 seed: 현재 KEYWORD_REGISTRY 에 있는 키워드 벌크 INSERT
3. lib/keyword-data.ts: KEYWORD_REGISTRY 대신 Supabase query 사용하도록 업데이트
4. 로컬 테스트 + Vercel preview 확인 후 main 머지

## Acceptance
- [ ] keyword_pages 테이블 Supabase Dashboard 에서 확인
- [ ] /categories/[slug] 페이지 DB 기반 렌더링 정상 동작
- [ ] KEYWORD_REGISTRY 하드코드 제거

## 의존성
없음 (migration 스크립트는 이미 main에 있음, commit 458a930)

## 참고
- 마이그레이션 파일: supabase/migrations/20260501_keyword_pages.sql
- 마이그레이션 스크립트: scripts/db-migrate.mjs (commit 458a930)
