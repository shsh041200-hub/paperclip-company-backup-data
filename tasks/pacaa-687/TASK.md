---
name: "[BE] old 카테고리 재분류 — plastic/flexible/glass/metal/eco → SG-1 (407건 즉시 편입)"
assignee: "backend-engineer"
---

## 배경

old 카테고리 스키마(paper/plastic/flexible/glass/metal/eco)에 남은 407건이 SG-1 커버리지에 계산되지 않음.
이미 새 ENUM 값들이 DB에 존재하므로, 정확한 매핑 검증 후 단순 UPDATE로 SG-1 커버리지를 즉시 높일 수 있다.

## 현황 (2026-05-14)

| Old category | Count | 권장 new category | Coverage 개선 |
|---|---|---|---|
| plastic | 256 | plastic_container | +256 → 340/2100 = 16.2% |
| flexible | 115 | flexible_packaging | +115 → 240/1700 = 14.1% |
| glass | 20 | glass_metal_container | +20 → 70/600 = 11.7% |
| metal | 16 | glass_metal_container | +16 → 86/600 = 14.3% |
| eco | 27 | flexible_packaging (추정) | +27 → 267/1700 = 15.7% |

total potential: 434건 즉시 SG-1 편입 가능 (추정 부정확시 제외 있을 수 있음)

## 작업

### Step 1 — 분류 검증 (dry-run, BE 단독)
- plastic 256건: subcategory / name 기반으로 plastic_container vs packaging_accessories 분류
- flexible 115건: flexible_packaging 직접 매핑 (subcategory 확인)
- glass 20건 + metal 16건: glass_metal_container (거의 확실, but spot-check 10건)
- eco 27건: flexible_packaging vs packaging_accessories 분류

### Step 2 — 매핑 SQL 생성
- category별 ID 목록 + UPDATE SQL (dry-run guard, ROLLBACK)
- before/after count 검증 쿼리 포함

### Step 3 — CEO 승인 + 적용
- 분류 결과 CEO에게 ask_user_questions (interaction) 제출
- 승인 후 production 적용

## DoD
- 400+ 건 SG-1 카테고리로 재편입
- pla
