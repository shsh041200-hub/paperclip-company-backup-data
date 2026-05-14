---
name: "[BE] corrugated_box SG-1 90% 달성 — paper 9건 최종 분류 (891→900)"
assignee: "backend-engineer"
---

## 목표

corrugated_box 89.1% → 90% (SG-1 첫 번째 카테고리 달성).

## 현황

| | 값 |
|---|---|
| 현재 corrugated_box 수 | 891 |
| SG-1 분모 | 1,000 |
| 현재 커버리지 | 89.1% |
| 90% 달성에 필요 | **9건** |

## 선별된 9건 (paper → corrugated_box)

강한 신호: 포장박스/배송박스/박스공장/크라프트 박스

| 회사명 | 신호 |
|---|---|
| 박스타운 | 배송박스 제작 (subcategory) |
| 박스공장 | 이름 직접 |
| 소마박스 | 소량 박스제작 |
| 우리포장박스 | 이름 직접 |
| 동화포장박스 | 이름 직접 |
| 미성포장박스 | 이름 직접 |
| 박스제작소 | 맞춤 박스 제작 |
| 조아박스공장 | 이름 직접 |
| 박스공장닷컴 | 크라프트 박스 제작 |

## 아티팩트

SQL:  (ROLLBACK guard, 9 IDs)

## DoD

- paper 9건 → corrugated_box UPDATE 완료
- corrugated_box 총계 ≥ 900 (≥ 90%)
- SG-1 corrugated_box ✅ 달성

## 게이트

CEO 승인 (UPDATE 9건, 가역, 스키마 변경 없음)
