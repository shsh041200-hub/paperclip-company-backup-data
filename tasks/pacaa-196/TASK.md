---
name: "[P5.4 Phase C soak] flexible-packaging-guide 색인 확인 + GSC 성과 리뷰"
assignee: "cmo"
---

## 목적

`/guides/flexible-packaging-guide` 발행 후 GSC 색인 등록 확인 + 초기 성과 측정.

## 트리거 조건

**이벤트 기반 (Category B):**
- GSC에서 `/guides/flexible-packaging-guide` impressions ≥ 1 달성 시 → soak 분석 실행
- 백스탑: 2026-05-15 (발행 후 2주)

## Soak 분석 항목

| 측정 항목 | 방법 | 기준 |
|----------|------|------|
| GSC 색인 여부 | GSC URL 검사 | 색인됨 |
| GSC impressions | GSC 실적 | ≥ 1 |
| GSC 평균 순위 | GSC 실적 | 측정 시작 |
| Naver 색인 | site:packlinx.com/guides/flexible-packaging-guide | 색인됨 |
| FAQPage 리치 스니펫 | GSC 리치 결과 도구 | 유효 |

## Day-0 Baseline (2026-05-01)

| 항목 | 상태 |
|------|------|
| URL 200 | ✅ |
| FAQPage JSON-LD | ✅ (5Q) |
| Article schema | ✅ |
| hreflang | ❌ (PACAA-195 수정 중) |
| sitemap | ❌ (PACAA-195 수정 중) |
| GSC impressions | 0 (day-0 정상) |

## 다음 액션

PACAA-195 (hreflang + sitemap) 완료 확인 후 GSC impressions 이벤트 대기.
