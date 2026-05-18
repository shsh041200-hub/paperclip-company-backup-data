---
name: "[O2-v4] Web-search-first enrichment — Naver webkr + Haiku LLM judge"
assignee: "backend-engineer"
---

## 목적
PACAA-786 v3 폐기 후속. 보드 결정 `965f8c68` (2026-05-18) = v4_web_search 채택. v3 의 multi-API map (Naver Local + Kakao Local) 접근은 **카테고리 mismatch** (지도 DB ≠ 공식 웹사이트 인덱스). 진짜 primitive 는 **Web Search API**.

부모: PACAA-784. 폐기됨: PACAA-786 (v3, branch `feat/match-sitemap-entry` commit `1e2c5a3` 머지 안 함).

## 아키텍처 (v4)
1. **Search primitive**: Naver **Web Search** API `/v1/search/webkr` (같은 NAVER_CLIENT_ID/SECRET, 같은 무료 quota)
2. **Query**: 회사명 단독, 필요시 카테고리 키워드 (포장/박스/완충재) 보강. **주소를 query 에 넣지 않음** — 보드 directive.
3. **Candidate pool**: webkr top-10 URL, 호스트 블랙리스트 (v3 의 ~80 도메인 재사용) 적용 후 top-3~5 채택
4. **Heuristic prefilter**: domain in blacklist 제거, 회사명 토큰 bigram 매칭 (음절수 동적 threshold v3 로직 재사용)
5. **LLM judge** (Claude **Haiku 4.5**): 각 candidate URL 의 page meta (title/description/og) fetch → 프롬프트에 회사명+**주소를 verification fact 로 주입**:
   > "이 페이지가 회사 '{name}' 의 공식 웹사이트인가? 검증 단서: 페이지에 주소 '{addr}' 또는 사업자번호 등이 등장하는가? Y/N + 0~1 confidence + 근거"
6. **Audit schema**: O1 과 호환 유지

## Acceptance Criteria
- v4 dry-run (limit=30, 100) 결과 보고: matched/false-positive/false-negative
- v4 matched rate ≥ v3 (16.7%) 비교표
- 월 운영비 ≤ $5 (실제 측정), 백로그 465건 일회성 ≤ $2
- ANTHROPIC_API_KEY/NAVER_CLIENT_ID/NAVER_CLIENT_
