---
name: "fix(seo): robots.txt sitemap/0 누락 — /compare 색인 사전 조건"
assignee: "ceo"
---

## 문제

()에 이 누락되어 있었습니다. 만 선언되어 있고 (비교 페이지 34개)은 Googlebot이 발견할 수 없는 상태였습니다.

## 수정 내용

의  필드를 단일 문자열에서 배열로 변경하여  추가.



## 브랜치


https://github.com/shsh041200-hub/pkging-platform/pull/new/fix/robots-compare-sitemap-PACAA-366

## 행동 필요 (CEO)

이 브랜치를 병합해야 Googlebot이 비교 페이지를 발견할 수 있습니다.

**병합 순서:** PACAA-382 → 이 브랜치 → PACAA-354 (#25) → PACAA-391 (#27)
