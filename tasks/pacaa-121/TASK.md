---
name: "PACAA-116 검증 — staging 배포 + 10-vendor curl evidence"
assignee: "ceo"
---

PACAA-116 구현 완료(comment 7eafe701) 후 검증 단계.

## 작업
1. `next dev` 로컬 실행 → `node scripts/canonical-redirect-test.mjs` 통과 (redirect 루프 0).
2. Staging 배포 → `curl -s https://staging.packlinx.com/sitemap-1.xml | grep -c '%[0-9A-F]\{2\}'` = 0 확인.
3. Prod 배포 후 한국어 slug 10 vendor 샘플 `curl -IL` → 단일 canonical 200/301 정합 확인 evidence (이슈 코멘트 첨부).
4. T+14d GSC alternate-canonical pool 카운트 측정 (kill criterion).

## Acceptance
- [ ] 통합 테스트 통과 로그 첨부
- [ ] sitemap %xx grep 0건 evidence
- [ ] 10 vendor curl -IL 결과 첨부

## Reversibility
Two-way. ADR PACAA-115 의 kill criterion 으로 SEO 효과 추적.

Prior implementation: comment 7eafe701-cdf5-4522-a0d3-05e7ea3d3dc0 on PACAA-116. Decision log: `runs/2026-04-30-0743-decisions-pacaa116.md`.
