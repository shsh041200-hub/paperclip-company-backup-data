---
name: "S1 — Sitemap-index 표준 구조 도입"
assignee: "cto"
---

## 배경

PACAA-573 보드 directive (코멘트 `dc272aad`): C1 후속 우선순위 C2 제외 전부 진행. S1 = sitemap-index 인프라 정리.

## 목표

현재 `/sitemap.xml` + `/sitemap/N.xml` shard 구조를 표준 `sitemap_index.xml` 패턴으로 마이그레이션. 자동 분할/재구성 안정성 확보.

## 현 상태

- 운영: `https://packlinx.com/sitemap.xml` + `/sitemap/1`, `/sitemap/2`, ... 형태 (shard 감사 메모리: feedback_sitemap_shard_audit_sweep)
- Next.js app router 의 sitemap.ts 다중 sitemap 패턴 사용 가능 (`generateSitemaps`)

## 작업

1. 현 `/sitemap.xml` + shards 라이브 sweep — entry 수 / shard 수 측정
2. Next.js `generateSitemaps` 기반 sitemap-index 도입 — `app/sitemap.ts` (또는 `app/(sitemaps)/sitemap.ts`) 재구성
3. robots.txt 가 sitemap-index URL 가리키도록 업데이트
4. PR 발의 → CEO dry-merge against origin/main → 머지
5. 프로덕션 verify: `curl /sitemap.xml` ≡ sitemap-index format, 각 shard 200 OK
6. GSC sitemap 재제출 (S2 와 별개)

## Acceptance

- [ ] sitemap.xml = `<sitemapindex>` 루트
- [ ] 각 shard URL 200 + valid `<urlset>`
- [ ] robots.txt sitemap 항목 업데이트
- [ ] PR 머지 + 라이브 verify

## 참고

- 메모리: feedback_sitemap_shard_audit_sweep / feedback_static_page_sitemap_acceptance / feedback_post_migration_literal_audit (CREATE TABLE 마이그레이션 X)
- PR 머지는 CEO 가 직접 (memory: feedback_ceo_executes_pr_merge)
