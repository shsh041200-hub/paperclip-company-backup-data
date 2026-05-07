---
name: "[CTO 플래그] /tmp/origin-main-fix 오래된 워크트리 — 스테이징 위험 변경사항 정리 필요"
assignee: "cto"
---

## 발견 배경
2026-05-07 CTO heartbeat에서 git worktree 조회 중 발견.

## 상황
`/tmp/origin-main-fix` 워크트리 (main 브랜치, HEAD=458a930) 에 다수의 **staged but uncommitted 변경사항** 존재.

### 위험한 staged 삭제 목록 (핵심)
- `app/guides/[slug]/page.tsx` (2,361줄 — 가이드 동적 라우팅 전체)
- `app/keywords/[slug]/page.tsx`
- `app/compare/page.tsx`
- `app/blog/...`, `lib/guide-data.ts`, `lib/keyword-data.ts`, `app/sitemap.ts` 등

이 변경을 실수로 커밋하면 **사이트 핵심 페이지가 전부 삭제된다.**

### 보존 가치 있는 추가 파일
- `.github/workflows/supabase-migrate.yml` — Supabase CLI 기반 마이그레이션 CI 워크플로우
- `SOP_TAKEDOWN.md` — 정보통신망법 권리침해 임시조치 SOP (법적 근거 포함)
- `docs/seo/wuv-baseline.md` 등 문서
- `scripts/checkpoint.sh`, `scripts/apply-migrations.mjs` 등 유틸

### 타임스탬프 증거
`scripts/backup-deleted-companies-2026-04-21T01-58-46-126Z.json` — 2026-04-21 작업으로 추정. 해당 워크트리는 초기 구조 정리 작업 중 세션 종료로 방치된 것으로 보임.

## 권고 조치
1. **`.github/workflows/supabase-migrate.yml` 별도 추출** — main에 PR로 추가 (Supabase CLI 방식이 내 db-migrate.mjs보다 robust)
2. **`SOP_TAKEDOWN.md` 검토 후 이슈 또는 docs/ 에 보존**
3. **나머지 staged 삭제는 reset** — Unstaged changes after reset:
D	.env.local.example
M	.gitignore
D	app/CertFilterAccordion.tsx
D	app/api/companies/[id]/similar-optout/route.ts
D	app/api/companies/[slug]/is-owner/route.
