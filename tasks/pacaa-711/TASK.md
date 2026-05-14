---
name: "[GSC Fix] 필터 URL 4,058건 canonical/noindex/cache 수정"
assignee: "cto"
---

## 배경

[PACAA-708](/PACAA/issues/PACAA-708) 진단 결과: packlinx.com 홈 필터 URL 4,058건이 GSC에서 "다른 4xx로 인해 차단됨"으로 기록됨.

**분류 결과: 전부 비의도적 차단** (의도된 차단 0건)

## 문제 요약

- URL 패턴: `/?industry=X&material=Y&form=Z&cert=W&moq=...` (필터 조합 수십만 ~ 수백만 가능)
- 원인 추정: `cache-control: private, no-cache, no-store` → CDN 미캐싱 → Googlebot 집중 크롤링 시 원본 서버 429
- 현재 상태: 동일 URL curl 200 반환 (과거 크롤 시 4xx)
- robots.txt: `/api/` 만 차단, 필터 URL 전부 크롤 허용됨 (의도치 않음)

## 필요 조치 (CTO)

1. **canonical 태그 추가**: 모든 `/?` 필터 URL 응답에 `<link rel="canonical" href="https://www.packlinx.com/">` 추가
2. **noindex 추가**: `X-Robots-Tag: noindex` 응답 헤더 or `<meta name="robots" content="noindex">` 추가
3. **캐시 수정**: 필터 URL `cache-control`을 CDN 캐싱 가능하도록 변경 (`public, s-maxage=60` 등)

## AC

- [ ] 필터 URL (/?industry=... 등) 응답에 canonical + noindex 적용
- [ ] Vercel CDN 캐싱 적용 확인 (x-vercel-cache: HIT)
- [ ] GSC 재검사 요청 후 4xx 건수 감소 확인 (2~4주 후)

## SEO 위험도

| 항목 | 심각도 |
|------|--------|
| 크롤 예산 낭비 | 고 |
| 중복/씬 콘텐츠 노출 | 고 |
| 확장 위험 (무한 조합) | 중 |
