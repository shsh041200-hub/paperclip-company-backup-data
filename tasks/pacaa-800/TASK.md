---
name: "[데이터 품질] 전화번호 역채움 법적 검토 — 1,175건 즉시 가능, PIPA KOR-371 게이트"
assignee: "ceo"
---

## 현황

vendor_candidates.phone 에 1,175건 전화번호 존재.
companies.phone 은 전부 NULL (0/2,767).

## 원인

PACAA-650 import_pipeline.py 에서 phone 필드 의도적으로 제외:
```python
# Allowed fields: name, address, category (phone omitted: KOR-371)
```

KOR-371 = PIPA 법적 검토 결과로 보임. 문서 확인 필요.

## 기술 구현

아래 SQL 한 번으로 즉시 적용 가능:
```sql
UPDATE companies c
SET phone = vc.phone, updated_at = NOW()
FROM vendor_candidates vc
WHERE c.candidate_source_id = vc.id
  AND c.phone IS NULL
  AND vc.phone IS NOT NULL;
-- 영향: ~1,175행
```

## 법적 질문 (CEO/LC 결정 필요)

1. **Naver Local API 약관**: 수집한 전화번호의 외부 서비스 재게시 허용 여부
2. **PIPA §15/§17**: 사업장 대표번호(02/031-xxx) vs 개인 휴대폰(010-xxx) 구분 기준
3. **공개 정보 예외**: 명함/업종별 협회지에 공개된 전화번호 → PIPA 공개 정보 예외 적용 여부

## 샘플 (전화번호 타입)

- 02/031/051-xxx: 사업장 유선 (공개 정보 가능성 高)
- 010-xxx: 모바일 (개인번호 가능성 — 별도 분류 필요)
- 070-xxx: 인터넷전화 (사업용 多)

LC 검토 후 사업장 번호만 선별 적용하는 방안도 가능.

## DoD

1. KOR-371 원문 또는 CEO 결정 기록
2. PIPA 적용 기준 명문화
3. 승인 시: UPDATE 실행 + migration 등록
4. 거절 시: import_pipeline.py 주석 업데이트
