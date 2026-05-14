---
name: "[BE] corrugated_box 8쌍 동명 중복 dedup — step5 import cross-category 정리"
assignee: "backend-engineer"
---

## 목표

PACAA-686 step5 import로 생성된 corrugated_box 레코드와 기존 paper 레코드 간 8개 동명 중복 쌍 분석 및 정리.

## 배경

[PACAA-688](/PACAA/issues/PACAA-688) 조사 중 발견:
- step5 import(2026-05-14 naver_local)가 8개 corrugated_box 레코드 신규 생성
- 기존 April paper 레코드와 동명으로 cross-category 중복 발생

## 대상 8쌍

| 회사명 | paper ID (구) | corrugated_box ID (신) |
|---|---|---|
| 박스타운 | 04f420cb | 77a457fe |
| 박스공장 | 07256ef1 | aeb3038b |
| 소마박스 | 08a2e725 | 3b00bf6b |
| 우리포장박스 | 2162838f | 44d8a2b3 |
| 동화포장박스 | 223761fc | 6bb5956e |
| 미성포장박스 | 2250102b | 70153ded |
| 박스제작소 | 31b817a7 | a8d8375e |
| 박스공장닷컴 | 5de5a93c | ebf00793 |

## 분석 방법

각 쌍에 대해:
1. phone/address/region 비교 → 동일 vendor 여부 판단
2. 동일 vendor: canonical = step5 import(naver_local 풍부) 유지, paper 측 archive(is_hidden=true)
3. 다른 vendor: 이름 disambiguate (지역명 추가 등)

## DoD

- 8쌍 동일/다른 vendor 판정 완료
- 동일 vendor: paper 측 is_hidden=true 처리 (CEO 승인 후)
- 다른 vendor: 이름 disambiguate 계획 수립
- corrugated_box 중복 쌍 0건 (is_hidden=false 기준)

## 후속

dedup 완료 후 90% 재도전 + 조아박스공장(3cfef38e) is_hidden 사유 확인 병행.
