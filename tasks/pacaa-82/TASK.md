---
name: "P2.5 선행 — 50 키워드 후보 리스트 + 보드 사인오프 (보강 4)"
assignee: "ceo"
---

## 배경

PACAA-80 보드 응답: "1. **50 키워드 사인오프** — P2.5 unlock". CEO가 50 키워드 후보 리스트를 작성하여 보드 사인오프 받는 것이 P2.5(programmatic SEO 50 랜딩 페이지) 선행 게이트(보강 4).

## 목표

8개 우선 카테고리 (PACAA-77 분모 카테고리 기준) × buyer-intent 모디파이어 mix로 50개 키워드 도출, 보드 사인오프 → P2.5 unlock.

## 산출물 (Definition of Done)

1. plan 문서: 50 키워드 후보 리스트 + 카테고리별 분배 + 모디파이어 전략 + 검증 방법
2. 본 이슈에 `request_confirmation` interaction 등록 → 보드 사인오프
3. 사인오프 후 본 이슈 close → PACAA-XX (P2.5 본 작업) 생성

## Owner

CEO 자체 수행. 키워드 전략은 CEO scope (CMO 미채용 상태). 검증 단계에서 Backend가 Naver Search Ads / Google Keyword Planner 데이터로 후보를 보강할 수 있으나, 우선 도메인 지식 + 벤치마크 기반 v1 후보를 보드에 제시하여 사인오프 시기를 단축.

## 의존성

- 선행: PACAA-26 (8개 카테고리 사인오프, done)
- 선행: PACAA-77 (커버리지 데이터, done) — 어떤 카테고리에 vendor density가 부족한지 파악
- 후속: P2.5 본 이슈 (PACAA-XX 생성 예정)

## Goal ancestry

SG-2 (한국어 패키징 핵심 50 키워드 SEO 점유율 40%) → 본 게이트 → P2.5
