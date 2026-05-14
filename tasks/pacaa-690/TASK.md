---
name: "[BE] step5 import 동명 vendor dedup — corrugated_box 8쌍 우선"
assignee: "backend-engineer"
---

## 배경

PACAA-686 step5 import 로 corrugated_box 카테고리에 vendor_candidates 출처 860 inserts. 그 결과 기존 `companies.category=paper` 의 일부 vendor 와 동명 corrugated_box 레코드가 cross-category 중복 발생.

PACAA-688 진단 (2026-05-14 01:41Z):
- 박스타운, 박스공장, 소마박스, 우리포장박스, 동화포장박스, 미성포장박스, 박스제작소, 박스공장닷컴 → 동명 corrugated_box 레코드가 step5 import 로 존재 (조아박스공장 제외 8건).

## 작업 범위

각 동명 쌍에 대해:
1. canonical 결정 — step5 import (vendor_candidates 출처, 신규 클린) 우선 가설.
2. 다른 레코드 분석 — phone/region/생성일/is_hidden/url 비교.
3. **동일 vendor 확정 시**: paper 측 레코드 archive (또는 step5 측에 merge — slug/url canonical 유지).
4. **다른 vendor 확정 시**: name disambiguation (회사명 뒤 지역/특화 추가).

기타: 다른 카테고리 (label_sticker, flexible_packaging 등) 의 step5 vs 기존 vendor 동명 쌍도 동일 패턴으로 scan.

## DoD

- 8 corrugated_box 동명 쌍 처리 결과 (canonical / merged / disambiguated) 보고.
- 다른 카테고리의 step5 동명 쌍 sweep 결과 (행 카운트).
- 후속: PACAA-688 90% chase 재개 (is_hidden 사유 확인 + 조아박스공장 처리).
