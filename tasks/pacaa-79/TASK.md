---
name: "P1.5.1 — naver_place 가비지 레코드 soft-delete (44건 + 전수 감사)"
assignee: "backend-engineer"
---

## 배경

[PACAA-78](/PACAA/issues/PACAA-78) P1.5 enrichment 실행 중 naver_place source 74건 중 44건이 실제 포장 업체가 아닌 가비지 레코드로 확인됨.

## 가비지 레코드 유형 (44건)

- 지명 단독: `경기도`, `대구광역시`, `충청북도`
- 지역 주소 단편: `경기도,파주시,파주읍`, `경기도,안산시 상록구`
- 블로그: `lbzezxyc님의 블로그`, `play_industry님의블로그`
- 사이즈 표기: `~50cm`, `100cm~200cm`, `200cm~`
- 음식점: `교동면옥 동탄레이크꼬모점`, `솔솥 판교점`
- 비포장 브랜드: `3M`, `노브랜드`

**공통 특징:** `source_attribution.enrichment_b_reverted = "garbage_phone_or_name"` 필드 설정됨.

## 작업 범위

### Phase 1 — 확인된 44건 soft-delete (CEO 승인 후)
```sql
UPDATE vendor_candidates
SET deleted_at = NOW()
WHERE source = 'naver_place'
AND source_attribution->>'enrichment_b_reverted' = 'garbage_phone_or_name'
AND deleted_at IS NULL;
```

### Phase 2 — naver_place 전수 감사
- 전체 naver_place 레코드에서 비업체 이름 패턴 탐지
- 추가 가비지 레코드 식별 및 soft-delete

### Phase 3 — 수집 파이프라인 필터 강화
- naver_scraper 에 업체명 유효성 검증 로직 추가
- 지명/블로그/음식점 패턴 필터 구현

## 의존성

- **선행:** CEO soft-delete 승인
- **관련:** [PACAA-78](/PACAA/issues/PACAA-78)

## DoD 영향

이 44건 삭제 시 score<0.6 잔존: 68 → **24건** (DoD <50 달성)
