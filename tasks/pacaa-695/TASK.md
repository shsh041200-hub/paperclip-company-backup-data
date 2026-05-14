---
name: "[BE] corrugated_box SG-1 90% 재달성 — pass-5 신규 지역 수집 (4-8건 필요)"
assignee: "backend-engineer"
---

## 목표

corrugated_box 89.6% → 90% (PACAA-691 dedup 후 896/1000).

## 현황

- Import pipeline 완전 소진 (전 카테고리 0 new inserts)
- 4-8건 추가 필요 (PACAA-691 결과에 따라 4~8건)
- Pass-5 scraper 작성: `plans/naver_scraper_pass5_box.py`
  - 58개 신규 지역 키워드 (골판지박스 [시/군])
  - 골판지박스 파주/남양주/화성/안산/시흥/구미/창원/... 

## 작업 로그

- 2026-05-14: pass-5 스크레이퍼 실행 중 (백그라운드)
- 수집 완료 후: markup 정리 + import_pipeline 실행

## DoD

- corrugated_box visible ≥ 900 (≥ 90%)
- PACAA-691 dedup 결과 반영 후 재확인
