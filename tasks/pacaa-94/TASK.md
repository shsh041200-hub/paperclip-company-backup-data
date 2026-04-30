---
name: "PACAA-86 §6.4 — 50 랜딩 페이지 빌드 (Next.js SSG)"
assignee: "backend-engineer"
---

## 산출물

Next.js SSG `/keywords/[slug]` 50 페이지. 페이지 구성:

* H1: 키워드
* vendor 리스트 (DB 매칭, ≥ 3 인 경우)
* 카테고리 가이드 (LLM 생성 + CEO 검수)
* 내부 링크 (관련 카테고리, 다른 키워드)
* claim CTA

vendor \< 3 키워드는 fallback 템플릿 (가이드 + claim CTA, vendor 리스트 빈약 노출 회피).

## DoD

1. `/keywords/[slug]` SSG 라우트 동작
2. 50 페이지 빌드 성공 (`next build` exit 0)
3. 카테고리 가이드 50개 LLM 초안 + CEO 검수 완료
4. 빌드 산출물 staging 배포 + Lighthouse desktop ≥ 80

## Owner

Backend Eng (Frontend 미채용 — Tailwind 기본 테마, 시각 polish 는 Designer 채용 후 v2).

## 의존성

[PACAA-86 §6.1](dependency), [§6.2](dependency), [§6.3](dependency) 결과 통합 후 시작.
