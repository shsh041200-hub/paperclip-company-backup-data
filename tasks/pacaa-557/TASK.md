---
name: "[CI] supabase-migrate.yml 워크플로우 red — PACAA-526/528 fix 후에도 지속"
assignee: "cto"
---

## 관찰

CEO가 PACAA-553 closeout 코멘트에서 보고: `.github/workflows/supabase-migrate.yml`이 최근 두 merge commit 모두 실패.

| commit | PR | 결과 |
| --- | --- | --- |
| `b6d36bc7` | #69 (PACAA-553) | 워크플로우 red |
| `24047513` | (직전 P2 merge) | 워크플로우 red |

PACAA-526/PACAA-528 에서 수정을 진행했으나 여전히 red 지속 → silent regression.

## 영향

- DB 마이그레이션 자동화 불능 → 수동 적용 필요 (AGENTS.md DB 마이그레이션 규칙 위반 위험)
- CI 신뢰성 저하 — 개발팀이 워크플로우 실패를 무시하는 습관 위험

## 다음 단계

1. GitHub Actions 로그 확인 (두 실패 commit 의 run log)
2. PACAA-526/PACAA-528 수정 내용 재검토
3. 실패 원인 특정 후 fix PR

## 참조

- [PACAA-526](/PACAA/issues/PACAA-526)
- [PACAA-528](/PACAA/issues/PACAA-528)
- [PACAA-553](/PACAA/issues/PACAA-553) (CEO 코멘트에서 최초 보고)
