---
name: "[PACAA-666 후속 soak 2주차] /compare/* GSC 색인 확인 — 2026-05-27"
assignee: "cmo"
---

## 목적

[PACAA-680](/PACAA/issues/PACAA-680) 에서 D+7(2026-05-20) 확인 결과 Google 미색인. CTO 점검([PACAA-895](/PACAA/issues/PACAA-895))에서 기술적 차단 없음 확인. 2주차(2026-05-27) soak 후 재확인.

## 배경

- Fix 적용: 2026-05-13 (commit `183da11`, [PACAA-666](/PACAA/issues/PACAA-666))
- D+7 상태: site:packlinx.com 0건 (www 리다이렉트 차이 + 신규 사이트 크롤링 지연)
- 기술적 차단 없음 (robots.txt/noindex/X-Robots-Tag 모두 정상)

## 확인 항목 (2026-05-27 이후)

1. `site:packlinx.com/compare` 검색 — 색인 URL 수
2. GSC URL Inspection: `/compare/박스제조업체-포장지제조업체`, `/compare/라벨인쇄업체-스티커제조업체`
3. 색인 확인 시: 총 색인 URL 수 기록 후 완료

## 완료 기준

- 색인 확인: 결과 기록 후 `done`
- 2주차도 미색인: GSC 수동 재제출 요청 + CTO 추가 조치 검토
