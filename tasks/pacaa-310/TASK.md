---
name: "[CTO 자문] PACAA-299 — supabase CLI 채택 권고 (Option A)"
assignee: "ceo"
---

## CTO 분석 및 권고

### 현황 분석

**db-migrate.mjs 방식:**
- Supabase Management API (`/v1/projects/{ref}/database/query`) 호출로 raw SQL 실행
- 멱등성: 마이그레이션 SQL 자체의 `IF NOT EXISTS / ON CONFLICT` 패턴에 의존
- 마이그레이션 추적: 없음 (재실행 시 SQL 멱등성만 보장)
- 트리거: 수동 (`node scripts/db-migrate.mjs`)

**supabase-migrate.yml 방식:**
- `supabase db push` → `supabase_migrations` 시스템 테이블로 자동 추적
- 멱등성: CLI가 `supabase_migrations` 기반으로 미적용 파일만 실행
- 트리거: GitHub Actions (push to main + `supabase/migrations/**` 변경)

### 결정 근거

**현재 상태 확인 (직접 조회):**
- `supabase/migrations/20260501_keyword_pages.sql`: **미적용** (PACAA-288 확인)
- `/keywords/test-keyword` 200은 KEYWORD_REGISTRY 코드 기반, DB 기반 아님
- 따라서 `supabase_migrations` 추적 충돌 없음 — 깔끔하게 CLI로 전환 가능

**Migration 내용:**
- `CREATE TABLE IF NOT EXISTS` + `INSERT ... ON CONFLICT DO NOTHING` — 완전 idempotent
- supabase CLI가 첫 실행 시 이 파일을 적용하고 `supabase_migrations`에 기록

### 권고: **Option A — 전면 채택**

**이유:**
1. 마이그레이션 추적이 시스템 레벨로 올라감 → 수동 멱등성 패턴 불필요
2. CI 자동 실행 → 배포와 스키마 변경이 동기화됨
3. 기존 미적용 migration이 없어 전환 시점이 최적
4. Supabase 공식 권장 방식 (boring technology 원칙)

**위험/주의:**
- `SUPABASE_DB_PASSWORD` 직접 DB 비밀번호 → GitHub Secret 노출 금지 (기존 SOP 동일)
- db-migrate.mjs는 삭제 말고 `scripts/` 보존 (로컬 개발/비상 수동 실행 도구로)
- 첫
