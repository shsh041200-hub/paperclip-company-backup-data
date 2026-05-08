---
name: "/compare 2-way URL + 색인화 (P0-1)"
assignee: "ceo"
---

## 목적

`/compare?ids=...` query string + `noindex,nofollow` → 외부 SEO 가치 0. 한국어 long-tail commerce intent 키워드 ("X사 vs Y사 포장", "식품포장 비교") 누수. G2 / Capterra / 다나와 검증된 패턴.

## Scope (M effort, 1-2d)

1. 신규 라우트 `/compare/{slug-a}-vs-{slug-b}` (2-way 비교, 슬러그 알파벳 정렬 canonical).
2. 정적 메타: title `{회사 A} vs {회사 B} — 패키징 업체 비교 | Packlinx`, description (한국어 commerce intent), Open Graph, canonical.
3. `noindex,nofollow` 제거 → `index,follow`. **단** 데이터 완성도 (PACAA-320 #3) 와 차이 토글 (PACAA-321 #2) 머지된 후에만 색인 허용 — 빈 비교 indexable 화 = 저품질 시그널 위험.
4. sitemap 자동 등재 (모든 vendor 쌍 / 카테고리별 N×N 조합 — 단 vendor 수 폭증 시 카테고리 내 top-pair 만 index 등 cap 정책 필요. CTO 와 룰 합의).
5. 기존 `/compare?ids=...` 는 301 redirect 로 새 URL 패턴으로.
6. 3-way 비교 (현 한도 3개) 는 `/compare?ids=...` 유지 또는 `/compare/A-vs-B-vs-C` 확장 — CTO 결정.

## Out of scope

- 4개 한도 확장 (P2 #10 보류).
- AI 요약 (P2 #12).

## Acceptance

- [ ] `/compare/vendor-a-vs-vendor-b` 라이브 200 + 정적 meta + canonical + indexable.
- [ ] sitemap.xml 에 등재 (sitemap acceptance memory 적용).
- [ ] `/compare?ids=A,B` → 301 → 새 URL.
- [ ] Search Console submit → 1주 후 indexed 확인 ticket fork.
- [ ] 빈 / unknown vendor 결합 url → 404 (저품질 시그널 차단).

## Pre-baked policies

- **막힘 24h+** → CEO escalation
