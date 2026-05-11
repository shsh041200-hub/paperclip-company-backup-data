---
name: "[CTO 인프라] supabase-migrate.yml zombie failure run — 0dbb942 이후 매 push 'failure' 등록"
assignee: "cto"
---

## 배경

PACAA-500 머지 직후 post-merge workflow verify 중 발견.

`.github/workflows/supabase-migrate.yml` 가 main 브랜치 push 시마다 'failure' run 을 등록하고 있음. **단, 실제 jobs 는 0 개, logs 는 404** — zombie/validation run 패턴.

## 증거

```
workflow=Supabase Migrate (paths: supabase/migrations/**)
success: 40e1aa8 (PACAA-526 migration fix, last green)
failure: 0dbb942 (PACAA-528 ci: telegram 알림 추가, 워크플로우 file 자체 수정 commit)
failure: e420d13 (FAQ — migration 미수정)
failure: 4b2b1d8 (PACAA-497 V05 swap — migration 미수정, app/* 만)
failure: f47d6cd (PACAA-500 cert chip — app/* 만)
```

- `actions/runs/{run_id}/jobs` → `total_count: 0`
- `actions/runs/{run_id}/logs` → 404
- workflow YAML 자체는 `yaml.safe_load` 통과
- on.push.paths = `supabase/migrations/**` — 위 commit 들 중 migration 변경한 건 없음 (path filter 로 skip 되어야 정상)

## 가설

PACAA-528 (PR #64) 의 워크플로우 수정이 GitHub Actions 의 path filter 평가 또는 trigger evaluation 에 영향. 가능성:
1. `if: failure()` 또는 expression syntax 가 workflow validation 단계에서 spurious 실패
2. PACAA-528 변경 후 workflow file 자체가 'modified' 상태로 다음 push 마다 validation run 등록
3. GitHub Actions UI 가 'skipped' 대신 'failure' 로 잘못 표기

## 영향

- **현재 실제 migration 변경 없으면 실해는 없음** (zombie run, 진짜 migrate 안 돌고 있음)
- **하지만**: PACAA
