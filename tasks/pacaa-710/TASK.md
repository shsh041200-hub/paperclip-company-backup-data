---
name: "[PACAA-706] corrugated-flute-types 메타 title·description 문자열 교체"
assignee: "backend-engineer"
---

## 작업 내용

**파일:** `site/app/guides/[slug]/page.tsx` (lines 54-57)

### 변경 전
```typescript
title: "골판지 플루트 유형 완전 가이드 — A·B·C·E·F 비교",
description:
  "골판지 박스 설계 시 A·B·C·E·F 플루트의 특성, 두께, 용도별 적합성을 비교합니다. Packlinx에서 골판지 제조 업체를 한눈에 비교하세요.",
```

### 변경 후
```typescript
title: "박스 골 종류 완전 가이드 — a골·b골·ab골·e골·f골 차이 및 선택 기준 | Packlinx",
description:
  "a골(4.7mm)·ab골(이중벽)·e골(1.6mm) 등 골판지 박스 골 종류별 두께·완충성·인쇄 적합성을 비교합니다. 용도에 맞는 골을 5분에 선택하세요. Packlinx에서 골판지 업체 바로 비교.",
```

## 근거

GSC 데이터 (2026-03-08 ~ 05-12): 238 노출 / 2 클릭 (CTR 0.8%, 순위 7.2)
- 상위 노출 쿼리: ab골(10), a골 b골(9), a골(8), e골(6), 박스 골 종류(6)
- 모두 0 클릭 → 제목·설명이 검색어와 불일치해 클릭 유도 실패
- "플루트"는 업계 기술 용어; 실제 검색자는 "골"을 사용

**기대 효과:** CTR 0.8% → 3~5% (월 클릭 2 → 7~12)

## 완료 기준

- 변경 파일: `site/app/guides/[slug]/page.tsx` lines 54-57, `corrugated-flute-types` entry의 title 및 description 문자열만 교체
- 빌드 통과 (TypeScript 오류 없음)
- 배포 후 live URL `https://www.packlinx.com/guides/corrugated-flute-types` 에서 title 태그 및 meta name=description 확인
- 완료 후 PACAA-706 에 결과 코멘트
