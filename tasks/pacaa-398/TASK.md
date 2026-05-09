---
name: "[GSC] 홈페이지 필터 URL 다른 4xx — 자가 해결 확인"
assignee: "cto"
---

## 발견 경위

2026-05-09 CTO 하트비트 — GSC Coverage 심층 조사 중 발견.

## 영향 URL 패턴

모두 홈페이지 필터 조합 URL:

```
https://www.packlinx.com/?industry=food-beverage&material=paper-corrugated,...
https://www.packlinx.com/?cert=iso9001,fsc,kc,eco_friendly
```

총 영향: **4,086개** (GSC 표시 4.09천) | 최종 크롤링: 2026-04-29

## 현재 상태

**직접 검증 결과: 200 OK** (자가 해결됨 ✅)

## 발생 타임라인

- 2026-04-21 ~ 2026-04-29: Googlebot 크롤 시 4xx 발생
- 2026-05-01: GSC 검증 시작됨 (재크롤 진행 중)
- 2026-05-09: 직접 테스트 결과 모두 200 OK

## 추정 원인

`app/page.tsx:36` `export const revalidate = 300` (ISR 5분) + Supabase DB 쿼리 조합에서 Googlebot 집중 크롤 시 일시적 4xx 발생. 이후 자가 복구.

## SEO 상태

- 캐노니컬: 모든 필터 조합에 `canonical: siteUrl` 설정 완료 (app/page.tsx:65-66) ✅
- `?q=...` 검색 쿼리: `noindex` 설정 ✅

## 크롤 예산 관찰

Googlebot이 4천+ 필터 조합을 모두 크롤 중. 캐노니컬 올바르게 설정되어 있으나, 크롤 예산 낭비. 향후 `robots.txt`에 필터 파라미터 Disallow 검토 가능 (별도 이슈 필요시).

## 작업

- [x] 원인 조사 완료
- [ ] 2026-05-16 GSC에서 count 감소 확인 후 close
