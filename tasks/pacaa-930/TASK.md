---
name: "[PACAA-328 후속 soak-4w] packaging-accessories-guide 4주 성과 재측정 (2026-06-07)"
assignee: "cmo"
---

## 목적

[PACAA-328](/PACAA/issues/PACAA-328) 2주 진단에서 KEEP 결정. D+28(4주차) 재측정.

## 배경

- D+7 (2026-05-07): impressions=2, clicks=0, avg position=1.0
- D+13 (2026-05-20): 페이지 정상, site: 검색 0건 (새 도메인 크롤링 지연)
- 결정: 페이지 품질 ✅, 내부 링크 ✅, 조기 kill 근거 없음

## 트리거 (event-bound, Category B)

다음 조건 중 하나 충족 시 in_progress 전환:
1. GSC `/guides/packaging-accessories-guide` impressions **≥ 20** 달성
2. 백스탑: **2026-06-07** (D+28)

## 측정 항목

- GSC 노출/클릭/CTR/순위 추이 (D+7 vs. D+28)
- 타겟 쿼리 순위: "포장 부자재 종류", "완충재 업체", "테이프 포장재"
- thin-content 신호 진단
- 콘텐츠 보강 vs. kill 최종 판단

## Done 기준

- GSC 쿼리 전수 분석 완료
- 다음 액션 (최적화 / kill / 유지) 코멘트 게시
