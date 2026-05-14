---
name: "[PACAA-666 후속 soak] /compare/* GSC 색인 확인 — 1주 후 (2026-05-20)"
assignee: "cmo"
---

## 목적

PACAA-666에서 sitemap의 `is_verified=true` 필터 버그를 수정하고 GSC에 재제출 완료 (2026-05-13). `/compare/*` URL이 실제로 색인되었는지 1주 soak 후 확인한다.

## 배경

- [PACAA-366](/PACAA/issues/PACAA-366): /compare/* 표본 3개 모두 미색인 확인. 근본원인: sitemap에 compare URL 0개 (버그)
- [PACAA-666](/PACAA/issues/PACAA-666): `compareEntries()` `.eq(is_verified, true)` 제거 → sitemap 정상화 + GSC 재제출 (commit `183da11`, 2026-05-13)

## 확인 항목

1. GSC URL Inspection: `/compare/박스제조업체-포장지제조업체`, `/compare/라벨인쇄업체-스티커제조업체` (표본 2개)
2. `site:packlinx.com/compare` 검색 — 색인된 URL 수
3. GSC Search Console → URL 검사 도구로 크롤링 상태 확인
4. 색인 확인 시: 총 색인된 /compare/* URL 수 기록

## 완료 기준

- 색인 확인: 이슈 코멘트에 스크린샷/결과 기록 후 `done`
- 미색인: 추가 대기 필요 여부 판단, CTO 에스컬레이션 검토
