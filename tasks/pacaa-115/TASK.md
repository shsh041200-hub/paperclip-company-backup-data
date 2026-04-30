---
name: "P1 SEO 정화: canonicalization + sitemap 1,000-cap 해제 + slug 중복 제거"
assignee: "cto"
---

PACAA-114 진단 결과 P0 트랙 후속. CTO refined analysis (2026-04-30) + 보드 승인 (PACAA-114 comment 741ee0e0, 옵션 A) 근거.

## 진단 요약 (input)

- 현재 sitemap: 1,031 URL (1,000-cap 의심) / 실제 벤더 ≥1,200
- GSC alternate-canonical pool: 12,785 (대부분 Korean encoded↔unencoded 쌍 추정)
- Slug dedup gap: 185/906 (20%) 가 `-NNNN` 숫자 suffix → vendor import 정규화 누락 흔적
- 5,667 "다른 4xx": 4/25 transient stale snapshot, 현재 prod에서는 모두 404 (이미 자체 보정됨)

## 작업 항목

### A. Canonicalization (12,785 alternate-canonical 정리)
1. URL canonical 정책 확정 — encoded vs unencoded (CTO 권고: Google 은 unencoded UTF-8 선호)
2. `<link rel="canonical">` + sitemap URL 모두 동일 정책으로 통일
3. 301 redirect: 비-canonical 변형 → canonical 단일 URL
4. 검증: 대표 10 URL 샘플 `curl -I`

### B. Sitemap 1,000-cap 해제
1. sitemap 생성 코드에서 `LIMIT 1000` 등 cap 제거 / 50,000-URL 분할 sitemap-index 도입
2. 전수 벤더 (≥1,200) 포함 보장 — 실제 카운트는 DB 쿼리로 확정
3. `lastmod` 필드 정확성 점검 (벤더 update 시 갱신되는지)
4. GSC `sitemap.xml` 재제출

### C. Slug 정규화 (185 `-NNNN` 중복)
1. vendor import 단계에서 slug 충돌 시 `-NNNN` 임의 suffix 대신 의미있는 식별자 사용 (지역/ID)
2. 기존 185개 `-NNNN` 슬러그: 가장 신뢰도 높은 1개 → canonical, 나머지 → 301 redirect
3. import 정규화 로직에 unit test 추가 (slug uniqueness + 의미성)

### D. GSC validation 요청
1. A/B/C 완료 후 GSC "다른 4xx 문제
