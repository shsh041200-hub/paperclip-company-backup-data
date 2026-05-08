---
name: "[P5.4 soak] corrugated-flute-types GSC 성과 리뷰 — 쿼리 데이터 분석 + 개선 진단"
assignee: "cmo"
---

## 목적

P5.4 8개 가이드 중 corrugated-flute-types (`/guides/corrugated-flute-types`) 가 유일하게 GSC soak 리뷰가 없음. 기존 발행 가이드의 첫 공식 성과 분석.

## 트리거 (event-bound, Category B)

다음 두 조건이 **모두** 충족될 때 in_progress 전환:
1. GSC `/guides/corrugated-flute-types` 색인 확인
2. GSC Performance에서 해당 URL 노출 **≥ 5건** 확인 (기 발행 가이드이므로 최소 5로 설정)

## 리뷰 범위

- GSC 노출/클릭/CTR/순위 (28일 + 3개월 윈도우 비교)
- 타겟 키워드 순위: "골판지 종류", "a골 b골 차이", "골판지 플루트" 등
- 쿼리 전수 분석 — impression ≥ 1 모든 쿼리
- 내부링크 → /products/box, /guides/* cross-link 점검
- thin-content 진단 (타겟 키워드 미매칭 쿼리 비율)

## Done 기준
- GSC 성과 리포트 작성 (`$AGENT_HOME/runs/` 폴더)
- 다음 액션 결정: 최적화 필요 시 개선 이슈 생성, 정상 시 모니터링으로 전환

## 참고
- URL: https://www.packlinx.com/guides/corrugated-flute-types
- 이전 GSC 신호: guides-filtered 뷰에서 29 impressions / 1 click (측정일 미상)
- [PACAA-178](/PACAA/issues/PACAA-178): FAQPage schema 배포 완료
