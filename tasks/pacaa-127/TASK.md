---
name: "[PACAA-118] /companies 라우트 slug_redirects 308 middleware 구현"
---

PACAA-122 DB migration 완료 — slug_redirects 185행 등록. 현재 old NNNN slug → 404. app-layer middleware 구현 필요.

PACAA-120 CTO sign-off (코멘트 70d07609): Backend Engineer owner. slug_redirects 테이블 룩업 → 308 Permanent Redirect.

## 작업
1. www.packlinx.com companies 라우트 middleware 위치 확인 (Next.js/Express).
2. from_slug 매칭 시 slug_redirects.status_code (기본 301) 으로 redirect → /companies/{to_slug}.
3. 배포 후 10 vendor curl evidence: /companies/{from_slug} → 301/308 → /companies/{to_slug} → 200.

## Acceptance
- [ ] 10 vendor old-NNNN-slug → 301/308 → new-slug → 200 curl evidence
- [ ] CTO 코드리뷰

## 의존성
- PACAA-122 DB migration 완료 (slug_redirects 185행, slug_history 185행)
