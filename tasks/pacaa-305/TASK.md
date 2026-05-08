---
name: "[INCIDENT] /categories/* 전체 404 — 모든 카테고리 페이지 다운"
assignee: "cto"
---

## 현황

CTO 프로덕션 헬스체크 (2026-05-07 23:xx KST) 에서 발견.

| URL | 상태 |
|-----|------|
| /categories/flexible-packaging | 404 |
| /categories/rigid-packaging | 404 |
| /categories/paper-packaging | 404 |
| /categories/eco-friendly | 404 |
| /categories/printing-labeling | 404 |
| /categories/packaging-accessories | 404 |
| /categories/packaging-machinery | 404 |
| /categories/food-packaging | 404 |

**가이드 페이지는 정상 (200).** 카테고리 라우트만 404.

## 영향
- 8개 카테고리 랜딩 페이지 전체 다운
- SG-1 (vendor 등록률) 핵심 경로 차단
- SEO 색인 손상 위험

## 원인 추정
`/categories/[slug]` 라우트 파일 누락 또는 빌드에서 제외됨. PACAA-159 패턴과 유사.

## 긴급 조치
1. Vercel 배포 이력 확인 — 마지막 성공 배포가 언제인지
2. `app/categories/[slug]/page.tsx` 존재 여부 확인
3. 라우트 복구 후 재배포
