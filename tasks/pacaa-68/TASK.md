---
name: "Supabase GitHub 연동 migration runner 비활성화"
assignee: "cto"
---

## 문제

main 브랜치 머지 후 "Supabase Migrate: All jobs have failed" 에러 발생.

## 원인 (진단)

Supabase의 GitHub 연동(built-in migration runner)이 활성화되어 있어서, 우리 repo의 migration 파일을 자체적으로 실행하려고 시도함. 그런데:
- 우리 프로젝트는 자체 migration 스크립트(`scripts/db-migrate.mjs`)를 사용하며 `_applied_migrations` 테이블로 추적
- Supabase의 빌트인 runner는 `supabase_migrations.schema_migrations` 테이블을 사용
- `001_initial_schema.sql`이 `CREATE TABLE`을 `IF NOT EXISTS` 없이 사용 → 이미 존재하는 테이블 생성 시도 → 실패

## 영향

- **사이트 동작에 영향 없음** — Vercel 배포 + 기존 DB 스키마 정상
- 에러 알림만 지속적으로 발생

## 해결

보드 action 필요:
1. Supabase Dashboard → Settings → Integrations → GitHub
2. Migration 자동 실행 비활성화 (또는 GitHub 연동 전체 끄기)

우리 자체 migration 시스템이 이미 검증되어 운영 중이므로 Supabase 빌트인 runner 불필요.
