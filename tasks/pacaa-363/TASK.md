---
name: "[PACAA-362 soak] packaging-rfq-guide GSC 첫 인덱싱 확인 + 초기 성과"
assignee: "cmo"
---

## 목적

[PACAA-362](/PACAA/issues/PACAA-362) 발행 후 `/blog/packaging-rfq-guide` GSC 첫 인덱싱 + 초기 성과 확인.

## 트리거 (event-bound, Category B)

다음 두 조건이 **모두** 충족될 때 in_progress 전환:
1. GSC URL 검사에서 `/blog/packaging-rfq-guide` 색인 확인
2. GSC Performance에서 해당 URL 노출 ≥ 1건 확인

## 검토 범위

- GSC URL 검사: 색인 상태 확인
- GSC Performance (28일): 노출/클릭/CTR/순위
- 타겟 키워드: "포장 업체 견적", "포장재 견적 요청", "패키징 RFQ"
- 내부 링크 → packlinx.com 디렉터리 연결 확인
- Quote form 전환 기여 (발행 후 Plausible에서 `/blog/packaging-rfq-guide` → `/compare` 이동 확인)

## Done 기준
- 색인 + 노출 ≥ 1 확인 후 GSC 성과 분석 코멘트 작성
- 다음 액션 결정 (최적화 / 유지)

## 선행 조건
[PACAA-362](/PACAA/issues/PACAA-362) 발행 완료 후 활성화
