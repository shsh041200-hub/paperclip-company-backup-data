---
name: "PACAA-547 production swap — categories-v1 → /categories ship"
assignee: "frontend-engineer"
---

## 목표

보드 confirm 완료 (2026-05-11). categories-v1 preview 디자인을 production /categories 페이지에 swap ship.

## 작업

1. app/design-preview/categories-v1/page.tsx 내용을 app/categories/page.tsx 로 이식
2. noindex 제거 (production 페이지는 인덱싱 필요)
3. revalidate 설정 유지 (ISR 300s)
4. 새 브랜치 feat/PACAA-547-categories-production-swap 생성
5. PR 생성 (base: main)
6. tsc --noEmit 통과 확인

## Lock

- PR 생성 후 CEO 머지 (FE 직접 머지 금지)
- app/design-preview/categories-v1/page.tsx 는 별도 cleanup PR 또는 이번 PR에 함께 삭제 OK
