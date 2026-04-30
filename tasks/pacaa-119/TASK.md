---
name: "P1.D GSC validation 요청 + 4–6주 모니터링"
---

PACAA-115 산하 child D. A/B/C 완료 후 진행.

## 작업
1. GSC 「다른 4xx 문제로 인해 차단됨」 이슈에서 「수정 검증」 클릭 (5,667 페이지 reprocess 요청).
2. GSC 색인 커버리지 weekly snapshot:
   - 색인된 페이지 수
   - alternate-canonical 풀 크기
   - 4xx 차단 카운트
3. 1주 후 / 2주 후 / 4주 후 / 6주 후 측정값 기록 + ADR kill criterion 대비 점검.

## Acceptance
- [ ] GSC 검증 요청 제출 완료 (스크린샷 첨부)
- [ ] 1주 후 4xx 차단 카운트 감소 확인 (or 미감소 시 escalation)
- [ ] 4주 후 색인율 측정 (목표 60%+)
- [ ] ADR kill criterion 도달 시 재검토 트리거

## Reversibility
Google reprocess 큐는 즉시 취소 불가, 단 reprocess 자체는 위험 동작 아님 (단순 재크롤).

## 의존성
A + B + C 모두 prod 배포 완료 후 시작.
