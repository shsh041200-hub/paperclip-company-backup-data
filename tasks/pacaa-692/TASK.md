---
name: "[BE] step5 동명 vendor bulk dedup — 945쌍 (주소 일치 765 자동 + 180 수동)"
assignee: "backend-engineer"
---

## 배경

[PACAA-690](/PACAA/issues/PACAA-690) sweep 결과: step5 import vs 기존 레코드 크로스카테고리 동명 쌍 **953건** 확인. 이 중 주소 완전일치 765건은 동일 vendor 확정. 8쌍은 PACAA-690에서 수동 처리 완료.

나머지 **945쌍** 자동/반자동 처리 필요.

## 범위

| 카테고리 쌍 | 건수 |
|-------------|------|
| corrugated_box × paper | 766 |
| paper × printing_postprocess | 32 |
| flexible_packaging × plastic_container | 28 |
| corrugated_box × packaging_accessories × paper | 26 |
| packaging_accessories × paper | 19 |
| 기타 | 82 |

- 주소 완전일치 (동일 vendor 확정): 765건 → 스크립트 자동처리 가능
- 주소 없거나 불일치: 180건 → 수동 검토 또는 name-based 휴리스틱

## DoD

1. 주소 일치 765건 bulk archive (step5 canonical 유지, older is_hidden=true)
2. 나머지 180건 검토 결과 (same / different / disambiguated 카운트)
3. 전체 dedup 후 non-hidden 업체 수 보고
