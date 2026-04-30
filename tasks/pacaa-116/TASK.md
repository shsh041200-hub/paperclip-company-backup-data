---
name: "P1.A canonical URL 정책 구현 — middleware + sitemap raw UTF-8 통일"
assignee: "cto"
---

PACAA-115 산하 child A. ADR (runs/2026-04-30-adr-canonical-url-policy.md) 채택 후 진행.

## 작업
1. Next.js middleware: percent-encoded vendor URL 요청 → `decodeURIComponent` 후 canonical raw UTF-8 path 로 301.
2. Sitemap generator: vendor URL 출력 시 raw UTF-8 사용 (XML escape 만, percent-encode 제거).
3. `<link rel="canonical">` 컴포넌트: SSR 시 정규화된 raw UTF-8 path 출력 보장.
4. 통합 테스트: 동일 vendor 의 encoded/unencoded 두 요청이 모두 200 raw 또는 301 → 200 raw 로 끝나는지 (redirect loop 차단).
5. 검증: prod 배포 후 대표 10 vendor URL `curl -IL` → 단일 canonical 200/301 정합.

## Acceptance
- [ ] middleware 통합 테스트 통과 (redirect 루프 0)
- [ ] sitemap 샘플에 percent-encoded URL 0건
- [ ] 10 vendor 샘플 curl 결과 첨부 (단일 canonical 수렴)

## Reversibility
Two-way (code 1시간 롤백). SEO 영향은 ADR 의 kill criterion 으로 트래킹.

## 의존성
ADR PACAA-115 acceptance 필요. Backend Engineer 복구 시 위임 가능 (현재 error 상태).
