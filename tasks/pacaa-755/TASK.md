---
name: "V1 디자인 메인 vendor 페이지 (`/companies/[slug]`) promote — 보드 결재 + 모니터링"
assignee: "ceo"
---

**부모**: PACAA-737 done (closeout 2026-05-16). V1 디자인 메인 라우트 promote 결재.

## 현재 상태
- V1 디자인 = `/internal/vendor-redesign/v1/[slug]` (noindex, preview only, robots.txt /internal/ Disallow)
- 메인 라우트 = `/companies/[slug]` (현재 디자인, sitemap 등재, 2767 vendor 색인됨)
- 분류 데이터 = `vendor_telesales_checks` 2767건 (found 41.8% / not_found 58.2%)
- 이의제기 채널 = `/vendor/dispute` + admin tool 라이브

## Promote 의 의미
- 모든 2767 vendor `/companies/[slug]` 페이지에 V1 디자인 + 분류 라벨 (기업 거래 전문 / 샘플·소량부터 가능) 적용
- 검색결과 (Google/Naver) 에 분류 라벨 노출 시작
- buyer 가 vendor 분류 본 후 클릭 패턴 변화 가능

## 옵션 3안

| 옵션 | 내용 | Cost | Risk | 학습 속도 |
|---|---|---|---|---|
| **즉시 promote** | 2767 vendor 모두 V1 디자인 일괄 적용 | 낮음 (FE route swap PR) | 중간 (분류 오류 광범위 노출 가능) | 빠름 (메트릭 전체 모집단) |
| **A/B test** | 50% vendor V1 / 50% 기존 — 메트릭 비교 후 결정 | 중간 (split routing + 메트릭 dashboard) | 낮음 (점진적) | 중간 (2주 메트릭 wait) |
| **보류** | preview 만 운영, 메인 적용 보드 추가 결재 후 | 0 | 0 | 0 (학습 없음) |

## CEO 권고
**즉시 promote** (옵션 1). 이유:
- 이의제기 채널 라이브 → 분류 오류 사후 회복 인프라 있음
- V1 디자인 효과 = 분류 표현 + Legal disclaimer + 신뢰 신호 → 즉시 부여
- A/B test 는 split routing complexity 비용 대비 학습 가치 한정 (분류 효과는 메트릭 보다 buyer feedback 으로 더 빠르게 확인)
- 보드가 risk 회피 우선이면 옵션 2 도 valid (Vercel 환경 변수 % split 으로
