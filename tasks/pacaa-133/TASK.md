---
name: "P2.5 — Next.js PoC 부트스트랩 (Vercel + 1개 키워드 라우트)"
assignee: "cto"
---

## 목표

[PACAA-87](/PACAA/issues/PACAA-87) 스택 결정(Next.js 16 App Router + Vercel Pro + Supabase Free) 확정에 따른 최소 PoC 부트스트랩.

## Scope (Phase 1 minimum)

- `npx create-next-app@latest` 으로 App Router 프로젝트 생성
- Vercel에 연결 (기존 Pro 구독 활용)
- 1개 키워드 라우트 예시: `/keywords/[slug]` — SSG or ISR
- `page.tsx` 에서 Supabase Free tier로 데이터 fetch 구조 잡기
- Backend가 데이터 API를 붙일 수 있는 hand-off 인터페이스: `GET /api/keywords/:slug` stub
- sitemap.xml, robots.txt, OG/canonical 기본 설정

## 인프라 제약 (보드 확인)

- Vercel Pro 기존 구독 → $0 추가
- Supabase Free tier 유지; 공간 부족 시 미사용 데이터 삭제 (업그레이드 X)

## Definition of Done

- Vercel에 배포된 URL 존재
- `/keywords/test-keyword` 라우트 200 응답
- Backend가 Supabase에서 데이터를 넣으면 페이지에 반영되는 구조 확인
- [PACAA-85](/PACAA/issues/PACAA-85) Backend Engineer에게 hand-off 완료

## Goal ancestry

[PACAA-87](/PACAA/issues/PACAA-87) → [PACAA-85](/PACAA/issues/PACAA-85) (SG-2 P2.5)
