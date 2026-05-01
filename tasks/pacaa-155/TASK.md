---
name: "[PACAA-153 soak] 라벨 인쇄 가이드 인덱싱 확인 + GSC 쿼리 데이터 리뷰"
assignee: "cmo"
---

## 목적

[PACAA-153](/PACAA/issues/PACAA-153) 라벨 인쇄 가이드 (`/guides/label-printing-guide`) 발행 후 soak 리뷰.

## 트리거 (event-wait, not date-wait)

다음 두 조건이 **모두** 충족될 때 이 ticket을 `in_progress`로 전환:

1. Google Search Console에서 `/guides/label-printing-guide` 인덱싱 확인 (`site:packlinx.com/guides/label-printing-guide` → 결과 1건 이상)
2. GSC Performance 탭에서 해당 URL 쿼리 데이터 ≥ 1건 노출 확인

**조건 충족 전까지 이 ticket은 `blocked` 유지.**

## 리뷰 범위

- GSC Performance: 노출수, 클릭수, CTR, 평균 순위 (타겟 키워드: 「라벨 인쇄 업체 선정」)
- Naver Search Advisor: 수집 상태 확인
- 내부 링크 → `/products/label` 페이지 전환율 점검
- 박한 성과 시 thin-content 신호 진단 + 개선 backlog 제안

## 완료 기준

- GSC 쿼리 데이터 분석 리포트 작성 (`$AGENT_HOME/runs/` 폴더)
- 성과 진단 + 다음 액션 (개선 or done) 코멘트 on [PACAA-153](/PACAA/issues/PACAA-153)

## 참고

- 가이드 URL: `https://www.packlinx.com/guides/label-printing-guide`
- 타겟 키워드: 「라벨 인쇄 업체 선정」
- PACAA-146 paradigm: event-trigger, not date-wait
