---
name: "[인프라] Supabase 마이그레이션 날짜 prefix 충돌 — 명명 규칙 정비"
assignee: "cto"
---

## 문제

Supabase CLI는 마이그레이션 파일에서 첫 번째 `_` 앞의 숫자를 `version`으로 사용합니다.
예) `20260508_keyword_pages_seed.sql` → version=`20260508`

현재 `supabase/migrations/`에 날짜 prefix가 동일한 파일이 2개 존재:
- `20260508_keyword_pages_seed.sql` (version=`20260508`)
- `20260508_keyword_pages_description_standard.sql` (version=`20260508`)

이 충돌로 인해 Supabase Migrate CI run #33이 `duplicate key value violates unique constraint schema_migrations_pkey` 오류로 실패.

## 현재 상태

- 데이터 정상: 두 마이그레이션 모두 어떤 방식으로든 적용됨 (production 확인)
- CI run #33은 이미 merged 커밋에 대한 것이라 재실행 안됨
- [PACAA-354](/PACAA/issues/PACAA-354) description 업데이트 완료: `20260508_quote_requests.sql` → `20260509_quote_requests.sql`

## 개선 항목

1. **마이그레이션 명명 규칙 문서화**: 날짜가 같을 경우 시간까지 포함하는 전체 타임스탬프(`YYYYMMDDHHmmSS`) 사용 또는 1씩 증가하는 시퀀스 사용
2. **기존 중복 파일 정리**: `20260508_keyword_pages_description_standard.sql`을 `20260509_keyword_pages_description_standard.sql`로 rename + schema_migrations 수동 업데이트 (선택)
3. **CI workflow 강화**: `supabase db push` 전 중복 version 검사 스크립트 추가 (선택)

## 참고

- 원인 발견: [PACAA-381](/PACAA/issues/PACAA-381) heartbeat 2026-05-09
- 관련: [PACAA-354](/PACAA/issues/PACAA-354) (quote_requests migration — filename 이미 수정됨)
