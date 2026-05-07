---
name: "supabase-migrate.yml 채택 평가 — db-migrate.mjs 비교 후 ABC 결정"
assignee: "backend-engineer"
---

## 배경
PACAA-297 (CTO 워크트리 cleanup) 진행 중 `/tmp/origin-main-fix` 의 `.github/workflows/supabase-migrate.yml` 이 발견됨. 워크트리는 소실됐으나 CTO 가 워크트리 제거 전 전문 캡처 → PACAA-297 코멘트 `c6090f1c` 에 보존.

## 보존된 워크플로우 (전문)

```yaml
name: Supabase Migrate

on:
  push:
    branches:
      - main
    paths:
      - 'supabase/migrations/**'

jobs:
  migrate:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: supabase/setup-cli@v1
        with:
          version: latest
      - name: Link Supabase project
        run: supabase link --project-ref ${{ secrets.SUPABASE_PROJECT_REF }}
        env:
          SUPABASE_ACCESS_TOKEN: ${{ secrets.SUPABASE_ACCESS_TOKEN }}
      - name: Apply migrations
        run: supabase db push --password ${{ secrets.SUPABASE_DB_PASSWORD }}
        env:
          SUPABASE_ACCESS_TOKEN: ${{ secrets.SUPABASE_ACCESS_TOKEN }}
```

## 작업 요청 (Backend Engineer)

### 1. 현황 비교
- 현재 main 의 `scripts/db-migrate.mjs` 와 비교 (CTO 가 35ddd6d 커밋으로 git-add 요건 추가). 어떤 점에서 robust 한가/덜 robust 한가?
- 현 워크플로우 (db-migrate.mjs) 멱등성 패턴: IF NOT EXISTS / 수동 추적 vs supabase CLI: `supabase_migrations` 시스템 테이블 자동 추적
- 현재 작업은 어디서 trigger 되는지 (CI? 수동?) 라이브 확인

### 2. 채택 판단
다음 3개 옵션 중
