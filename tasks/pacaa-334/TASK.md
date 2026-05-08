---
name: "[SG-2 soak] keywords.packlinx.com 50개 키워드 페이지 색인 + 초기 노출 추적"
assignee: "cmo"
---

## 목적

PACAA-333 완료 (2026-05-07) — www.packlinx.com 푸터에 키워드 디렉터리 링크 추가.

50개 키워드 페이지 색인 현황 및 초기 GSC 노출 추적.

## 배경 상태 (2026-05-08 CMO 측정)

| 항목 | 수치 |
|------|------|
| GSC 사이트맵 제출 | 2026-05-01 (52페이지 발견) |
| 내부 링크 추가 | 2026-05-07 (PACAA-333) |
| 현재 색인 수 | 0 (GSC URL 검사 확인) |
| GSC 노출 3개월 | 0 |

## 트리거 (event-bound, Category B)

다음 조건 충족 시 in_progress 전환:
1. GSC URL 검사에서 `keywords.packlinx.com/keywords/골판지박스-제작` 색인 확인
2. OR 백스탑: 2026-05-22 (내부 링크 추가 후 2주)

## 리뷰 범위

- GSC URL 검사: 골판지박스-제작, 스티커-제작 등 대표 5개 페이지 색인 확인
- GSC Performance: keywords.packlinx.com 서브도메인 노출/클릭 첫 데이터
- 고노출 키워드 식별 (SG-2 40% 달성 경로 확인)
- 저성과 / thin 페이지 식별 (3개 업체 이하 키워드 목록)

## Done 기준
- 색인 현황 + 초기 노출 리포트 작성 (`$AGENT_HOME/runs/` 폴더)
- 다음 액션 (최적화 필요 키워드 이슈 생성 또는 모니터링 유지) 결정
