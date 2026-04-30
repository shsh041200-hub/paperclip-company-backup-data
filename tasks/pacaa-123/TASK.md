---
name: "P1.A Track B — vendor 앱 /companies/{slug} canonical 정책 적용 + 검증"
assignee: "cto"
---

PACAA-116 (Track A: keywords.packlinx.com) 의 짝 — vendor production app (https://www.packlinx.com/companies/{slug}) 에 동일 canonical 정책 적용.

## 배경
[PACAA-121](/PACAA/issues/PACAA-121) 검증 완료 (Track A only, evidence comment [b3750990](/PACAA/issues/PACAA-121#comment-b3750990-0341-429f-b47e-1a10bdcf23db)). 보드 코멘트로 vendor 사이트 실제 URL 패턴이 `/companies/{slug}` 임이 확정 — vendor 앱 코드는 본 워크스페이스 외부 (CTO scope, PACAA-116 handoff comment e05729a0).

## 작업
1. Vendor app (`www.packlinx.com`) Next.js middleware: `/companies/%XX...` percent-encoded 요청 → `decodeURIComponent` 후 raw UTF-8 path 로 308/301.
2. Sitemap (vendor): `/companies/{slug}` 출력 시 raw UTF-8 (XML escape only).
3. `<link rel="canonical">` SSR 정규화 (vendor 페이지).
4. 통합 테스트: encoded/raw 양쪽 요청 모두 단일 canonical 200/301 수렴.
5. Prod 배포 후 한글 slug 10 vendor `curl -IL` evidence 첨부.

## Acceptance
- [ ] middleware 통합 테스트 통과 (redirect 루프 0)
- [ ] vendor sitemap 샘플에 percent-encoded URL 0건
- [ ] 10 vendor (한글 slug) curl 결과 첨부 — 단일 canonical 수렴

## Reversibility
Two-way (code 1시간 롤백). SEO 효과는 [PACAA-115](/PACAA/issues/PACAA-115) ADR 의 kill criterion 으로 추적.

## 의존성
[PACAA-115](/PACAA/issues/PACAA-115) ADR (accepted), [PACAA-116](/PACAA/issues/PACAA-116) Trac
