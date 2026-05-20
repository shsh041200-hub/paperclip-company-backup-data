---
name: "Supabase RLS enable — 6 public tables (PACAA-948 spawn)"
assignee: "cto"
---

보드 결정 (PACAA-948 interaction 5c47ca0c): 옵션 A — CTO 위임, 6 RLS-disabled public 테이블 모두 RLS enable + 테이블별 policy 설계 후 Supabase Migrate workflow PR.

## 대상 테이블 (advisor 2026-05-17 캡처)
프로젝트: pkging-platform (`jnrciibwtutzymkoepfp`)

1. `public.korean_search_synonyms`
2. `public.crawl_ai_usage`
3. `public.use_case_tags`
4. `public._applied_migrations`
5. `public.slug_redirects`
6. `public.slug_history`

## 설계 지침 (CEO/보드 가이드)
- **Reference 데이터** (`korean_search_synonyms`, `use_case_tags`, `slug_redirects`, `slug_history`): FE 에서 anon 으로 read 필요한지 사용 패턴 확인 후, 필요 시 `SELECT` only anon policy + `INSERT/UPDATE/DELETE` 는 service_role only.
- **Internal 데이터** (`crawl_ai_usage`, `_applied_migrations`): 전체 service_role only. anon read 금지.
- 사용 패턴 모호하면 CEO 통해 보드 재confirm 가능 (over-restrict 로 site 깨지지 않게).

## Acceptance
- [ ] 6 테이블 모두 `ALTER TABLE ... ENABLE ROW LEVEL SECURITY;` 마이그레이션 작성
- [ ] 테이블별 policy SQL 작성 (위 지침 따름)
- [ ] PR 생성 (Supabase Migrate workflow) — pkging-platform repo
- [ ] PR 머지 후 Supabase Security Advisor 재실행 → 6 ERROR 모두 사라짐 확인 (CEO 또는 보드 캡처 가능)
- [ ] FE / Backend 호출 sanity check (RLS 후 site/route 깨지지 않음)

## 참고
- Supabase Migrate workflow 경로: `~/.paperclip/.../pkging-platform/sup
