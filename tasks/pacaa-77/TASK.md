---
name: "P1.2 ext — 저커버리지 7개 카테고리 추가 vendor 수집"
assignee: "backend-engineer"
---

## 배경

[PACAA-70](/PACAA/issues/PACAA-70) P1.3 dedup 완료 후 커버리지 현황:

| category | coverage_n | denominator | coverage% |
|----------|------------|-------------|-----------|
| corrugated_box | 888 | 1,000 | 88.8% ✅ |
| flexible_packaging | 240 | 1,700 | 14.1% 🔴 |
| glass_metal_container | 86 | 600 | 14.3% 🔴 |
| label_sticker | 182 | 3,160 | 5.8% 🔴 |
| packaging_accessories | 197 | 3,425 | 5.8% 🔴 |
| packaging_machinery | 82 | 320 | 25.6% 🔴 |
| plastic_container | 275 | 2,100 | 13.1% 🔴 |
| printing_postprocess | 294 | 17,558 | 1.7% 🔴 |

SG-1 목표(90%) 달성을 위해 7개 카테고리 대규모 추가 수집 필요.

## 목표

우선순위 카테고리(gap이 크고 분모 규모가 작은 것 먼저)의 vendor target list를 추가 수집하여 coverage 90% 달성 가능 수준으로 끌어올린다.

## 우선순위 (분모 대비 gap 기준)

1. **packaging_machinery**: 320 분모, 82 보유 → 238개 추가 필요 (달성 가능성 높음)
2. **glass_metal_container**: 600 분모, 86 보유 → 454개 추가 필요
3. **flexible_packaging**: 1,700 분모, 240 보유 → 1,290개 추가 필요
4. **plastic_container**: 2,100 분모, 275 보유 → 1,615개 추가 필요
5. **label_sticker**: 3,160 분모, 182 보유 → 2,660개 추가 필요
6. **packaging_accessories**: 3,425 분모, 197 보유 → 2,885개 추가 필요
7. **printing_postprocess**: 17,558 분모, 294 보유 → 14,507개 추가 필요 (분모 재검토 필요)

> printing_postprocess 분모(17,558)는 전체 인쇄업 포함으로 과대추정 가능성. 라
