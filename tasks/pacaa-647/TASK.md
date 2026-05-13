---
name: "[BE] SG-1 커버리지 갭 진단 — vendor_candidates 1,378건 미승인 + 4개 카테고리 미지원"
assignee: "ceo"
---

## 발견 (2026-05-13 데이터 레이어 전략 점검)

### 현황

Packlinx 디렉터리(companies 테이블)의 현재 카테고리별 업체 수:

| 카테고리 | companies 수 |
|---|---|
| paper (corrugated_box) | 945 |
| plastic (plastic_container) | 253 |
| flexible (flexible_packaging) | 114 |
| eco (eco-friendly) | 27 |
| glass | 20 |
| metal | 15 |
| label_sticker | **0** |
| printing_postprocess | **0** |
| packaging_accessories | **0** |
| packaging_machinery | **0** |

### 핵심 갭

**vendor_candidates 테이블에 1,378건의 clean (dedup 통과) naver_place 미승인 후보가 존재한다:**

| 카테고리 | clean 후보 수 |
|---|---|
| printing_postprocess | 349 |
| label_sticker | 270 |
| packaging_accessories | 230 |
| flexible_packaging | 177 |
| packaging_machinery | 174 |
| plastic_container | 108 |
| glass_metal_container | 70 |
| **합계** | **1,378** |

**데이터 품질 (200건 샘플):** 전화번호 84%, 주소 80.5%, 양방향 보유 74.5%

### 문제

1. **4개 카테고리(label_sticker, printing_postprocess, packaging_accessories, packaging_machinery)는 companies.category 값이 없어 현재 Packlinx 디렉터리에서 지원되지 않는다.** SG-1 목표(8개 카테고리 90%) 달성 불가 상태.

2. **1,378건의 clean 후보가 PACAA-77 수집 이후 미승인 상태로 vendor_candidates에 방치.**

3. flexible_packaging(177건), plastic_container(108건), glass_metal_container(70건)은 지원 카테고리지만 역시 미승인.

## 제안 (CEO 방향
