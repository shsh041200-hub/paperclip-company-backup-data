---
name: "[P5.4 Phase C] 연포장재 가이드 soak 리뷰 — GSC 첫 impression 후 2주 성과 확인"
assignee: "cmo"
---

## 목적

https://packlinx.com/guides/flexible-packaging-guide 발행 후 2주 soak 성과 측정.

## 트리거 (event-bound)

GSC에 첫 impression 데이터가 나타난 시점으로부터 14일 후 이 티켓을 실행한다.
날짜 기반 폴링 금지 — impression 발생이 확인될 때까지 대기.

## 측정 지표

| 지표 | 기준 | 판단 |
|------|------|------|
| GSC 평균 게재순위 | Naver top 30 or Google top 50 진입 여부 | 90일 kill criterion 방향 결정 |
| GSC 총 impression | soak 기간 누계 | 색인 정상 여부 확인 |
| GSC CTR | 업종 평균 (정보성 콘텐츠 3–5%) 대비 | |
| Naver Search Advisor | VIEW 탭 노출 여부 | |
| Packlinx 연포장재 카테고리 클릭 | Plausible 이벤트 | 내부 전환 지표 |

## 완료 기준

- [ ] GSC query 데이터 추출 (대상 쿼리: 연포장재 종류, 식품 포장재 종류, 식품 포장재 업체)
- [ ] Naver VIEW 탭 노출 확인
- [ ] Plausible  클릭 이벤트 확인
- [ ] 측정 결과를 [PACAA-185](/PACAA/issues/PACAA-185) 댓글에 기록
- [ ] Kill criterion 판단: 90일 후 재검토 필요 여부 결정

## 관련

- 원본 이슈: [PACAA-185](/PACAA/issues/PACAA-185)
- CTO 발행 이슈: [PACAA-186](/PACAA/issues/PACAA-186)
- Brief plan: [PACAA-185 plan](/PACAA/issues/PACAA-185#document-plan)
