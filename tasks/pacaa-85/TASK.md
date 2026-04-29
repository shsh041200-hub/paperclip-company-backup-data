---
name: "P2.5 — 50 키워드 programmatic SEO 랜딩 페이지 구현"
assignee: "backend-engineer"
---

## 배경

2026-04-29 PACAA-80 interaction `53989d76` 보드 사인오프 완료(승인). 50 키워드 v1 리스트 확정 — PACAA-80 댓글 `79b88309` 본문 참조.

## 목표

승인된 50 키워드 각각에 대해 programmatic SEO 랜딩 페이지를 생성하고 양 검색 엔진(Naver Search Advisor + Google Search Console — PACAA-81에서 연결 완료)에 sitemap 제출하여 indexing 시작.

## Definition of Done — 단계별

### Phase 1 — Proof of Concept (1 키워드 end-to-end)
1. 1개 키워드(추천: "골판지 박스 제작" — coverage 88.8%로 vendor density 가장 높아 콘텐츠 풍부)에 대해 SSR 또는 MDX 라우트 구현.
2. 페이지 구성: H1(키워드 포함) + 카테고리 설명 + 매칭 vendor 목록(top 10~20) + CTA.
3. SEO 기본 — meta title/description, schema.org `LocalBusiness` or `ItemList`, canonical URL, OG tags.
4. 본 이슈 댓글로 PoC URL + Lighthouse SEO 점수 보고.

### Phase 2 — 49 키워드 일괄 생성
5. Phase 1 템플릿을 기반으로 나머지 49 키워드 페이지 생성. 키워드 → 카테고리 매핑은 PACAA-80 `79b88309` 댓글 본문의 카테고리 분류를 정답지로 사용.
6. 각 페이지 vendor 매칭 — 카테고리 기반 query로 자동 필터, 결과가 < 5개인 키워드는 본 이슈 댓글에 flag.
7. 50/50 페이지 production deploy.

### Phase 3 — Search Engine Submission
8. `sitemap.xml` 자동 생성 — 50 신규 라우트 포함.
9. Google Search Console에 sitemap 제출, indexing request.
10. Naver Search Advisor에 sitemap 제출 (PACAA-81에서 연결 완료된 채널).
11. 본 이슈 댓글로 두 엔진 submission 확인 + 첫 indexing 수신 시점 기록.

## 측정 / 성공 기준 (Goal `bddc2a78` 기준)

- **성공:** 50/50 index
