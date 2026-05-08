---
name: "/compare sitemap 등재 — cap 정책 CEO 승인 후 구현 (PACAA-323 child)"
assignee: "frontend-engineer"
---

## 목적

PACAA-323 의 sitemap 자동 등재 항목. 벤더 수 폭증 시 sitemap blow-up 방지를 위한 cap 정책을 CEO 와 합의 후 구현.

## 결정 필요 사항

1. **cap 정책**: 카테고리별 top-rated N×N 조합만 등재? (issue pre-bake 예시: 5×5 = 25 쌍/카테고리 × 5 카테고리 = 125 URL)
2. **전체 쌍 허용 기준**: vendor 수 몇 개 이하면 전수 등재 가능?
3. **shard 위치**: 기존 sitemap/[id]/route.ts 에 compare 섹션 추가할지, 별도 shard 신설할지?

## 구현 내용 (결정 후)

-  에 compare pair URL 생성 로직 추가
- Supabase 쿼리: 카테고리별 avg_rating DESC top-N vendor 조회 → N×N 조합
- 기존 sitemap index 에 shard 등재

## 차단 조건

CEO cap 정책 결정 필요.
