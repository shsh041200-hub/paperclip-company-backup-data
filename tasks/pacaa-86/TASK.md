---
name: "P2.5 — 50 키워드 programmatic SEO 랜딩 페이지 (실행)"
assignee: "frontend-engineer"
---

## 배경

[PACAA-82](/PACAA/issues/PACAA-82) 50 키워드 v1 plan 보드 사인오프 완료 (2026-04-29 09:55 UTC). P2.5 unlock.

## 목표

50 키워드 × 랜딩 페이지 (programmatic SSG) → 90일 내 ≥20개 SERP top 10 (SG-2 40% 매칭).

## 산출물 (Definition of Done)

1. **§6.1 볼륨 검증** (1주차): 50 키워드 + 예비 풀 10개를 Naver Search Ads + Google Keyword Planner 로 측정. 볼륨 ≥ 50 & 경쟁도 low~medium 통과 50개 확정. 측정 결과를 plan 문서에 §12로 추가.
2. **§6.2 vendor density 매핑** (1~2주차): 각 키워드 → 우리 DB vendor 매칭 카운트. 매칭 < 3 인 키워드는 "카테고리 가이드 + claim CTA" 템플릿 fallback 표시.
3. **§6.3 SERP 경쟁 검증** (CEO 수동, 2주차): 상위 10 결과 디렉토리/리스트 페이지 ≥ 3 = 침투 가능. 단일 vendor 사이트 독점 키워드는 §7 예비 풀에서 교체.
4. **랜딩 페이지 50개 빌드** (3~4주차): Next.js SSG, route 패턴 `/keywords/[slug]`. 페이지 구성:
   - H1: 키워드
   - vendor 리스트 (우리 DB 매칭, ≥3 인 경우)
   - 카테고리 가이드 (LLM 생성 + CEO 검수)
   - 내부 링크 (관련 카테고리 페이지, 다른 키워드 페이지)
   - claim CTA
5. **인덱싱** (4~5주차): sitemap.xml 등록, Search Console + Naver Advisor submit. 첫 인덱싱 5일 이내 ≥40 페이지 인덱스.
6. **측정 cadence** (8주~): 주간 SERP rank 트래킹 (50 키워드). 8주차 보드 리뷰 — top 30 < 10 이면 일시정지 + 재구성. 12주차 = 90일 success/kill 결정.

## Owner

Backend Eng (단독 가능). Frontend 미채용 상황 — Next.js SSG 로 진행. Designer 부재 시 기본 Tailwind 테마 사용, 시각적 polish 는 페어 3 (Designer) hire 후 v2.

## 의존성

- 선행 done: [PACA
