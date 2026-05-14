---
name: "[BE] corrugated_box vendor_candidates 878건 임포트 — SG-1 Step 5"
assignee: "ceo"
---

## 배경

PACAA-682 Step 5 — corrugated_box vendor_candidates 878건 임포트 (PACAA-682 연속 작업)

PACAA-650 import_pipeline이 CATEGORY_MAP에서 `corrugated_box`를 제외했기 때문에 899건의 vendor_candidates (category_id = corrugated_box)가 companies 테이블에 임포트되지 않았다.

- PACAA-682에서 ENUM 추가 완료 ✅ (corrugated_box 이제 category_type에 존재)
- PACAA-682 Step 3: 기존 paper 29건 → corrugated_box 재분류 완료 ✅

## 현재 상태

| 항목 | 값 |
|------|-----|
| vendor_candidates (corrugated_box, clean) | 878건 |
| vendor_candidates (corrugated_box, duplicate) | 11건 |
| vendor_candidates (corrugated_box, merged) | 10건 |
| companies.corrugated_box (현재) | 29건 |
| SG-1 corrugated_box 커버리지 (현재) | 2.9% (분모 1,000) |

## 작업 범위

### Step 5a — import_pipeline.py CATEGORY_MAP 수정
```python
# scripts/import_pipeline.py의 CATEGORY_MAP에 추가:
"corrugated_box": "corrugated_box",
```

### Step 5b — Dry-run (before/after 카운트)
```bash
python3 scripts/import_pipeline.py  # dry-run 기본값
```
예상: ~850건 신규 companies (878건 중 일부 dedup으로 제외 가능)

### Step 5c — CEO 승인 후 --apply 실행
```bash
python3 scripts/import_pipeline.py --apply
```

## DoD

- import_pipeline.py CATEGORY_MAP에 corrugated_box 추가 + dry-run PASS
- CEO 승인 후 878건 임포트 실행
- companies.corrugated_box: 29 → ~880건
- SG-1
