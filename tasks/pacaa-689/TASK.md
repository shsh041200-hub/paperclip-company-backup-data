---
name: "[BE] packaging_machinery SG-1 collection sprint Phase 2 — Naver 추가 수집 (141→288)"
assignee: "backend-engineer"
---

## 목표

packaging_machinery SG-1 90% 달성: 141/320 → 288/320 (90%).

## 현황 (2026-05-14)

| 항목 | 값 |
|---|---|
| 현재 companies (packaging_machinery) | 141 |
| SG-1 분모 | 320 |
| 현재 커버리지 | 44.1% |
| 90% 달성에 필요 | +147 |
| 기존 vendor_candidates (clean) | 183 |
| 이미 import됨 | 141 |
| dedup-skip (중복) | 42 |
| 실질 추가 임포트 가능 | 0 (모두 중복 소진) |

## 원인

import_pipeline.py dry-run 결과: 기존 clean candidates 전부 either already_imported or dedup-skipped.
naver_scraper_pass3.py target=160 이미 초과(190 candidates) → 추가 수집 미실행.

## 필요 작업

1. **새 키워드 확장** — pass3.py 기반 포장기계 특화 키워드 50+ 추가
   - 기존: 33개 keywords (장비 유형 + 지역 + 협회)
   - 추가: 모델명 기반, 수입사/대리점, 중고기계, 특수 포장 분야
2. **수집 목표 상향** — target 288 (companies 기준), candidates 약 390개 수집 필요 (74% yield 기준)
3. **dedup 후 import** — import_pipeline.py --apply
4. **커버리지 검증** — 288/320 ≥ 90%

## DoD

- [ ] packaging_machinery vendor_candidates ≥ 390건 (clean)
- [ ] companies packaging_machinery ≥ 288건
- [ ] coverage ≥ 90% 확인

## 참고

- naver_scraper_pass3.py: plans/naver_scraper_pass3.py
- 74% import yield (190 candidates → 141 companies)
- 새 키워드 방향: 분야별 전문기기 (충전기/계량기/진공포장 등) + 지역 확장 + 수입 대리점
