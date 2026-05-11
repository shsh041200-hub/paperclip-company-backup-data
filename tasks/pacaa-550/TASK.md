---
name: "PACAA-490 P5 — faq 페이지 UX/UI polish"
assignee: "frontend-engineer"
---

## Context

부모: PACAA-490, P5. P4 guides 완료 후 트리거. 시퀀스 최종.

## 의도

faq \= supportive content, traffic 적지만 trust 시그널 보조. 작은 polish.

## 작업 방식

Lean polish:

1. 라이브 audit `/faq`
2. UX 갭 (가독성, 앵커 link, 검색·필터, mobile reading, 관련 가이드/카테고리 cross-link)
3. 단일 개선안 preview `/design-preview/faq-v1`
4. CEO surface → 보드 confirm → production swap

## 포커스

* 앵커 link + URL hash deep-link
* 카테고리 grouping (vendor / 운영 / 결제 등)
* 검색·필터 (필요 시)
* 관련 가이드 / vendor cross-link surface
* 모바일 reading 위계

## Lock

* V05 토큰, 헤더/푸터 production, /app/faq production 변경 0, noindex meta
* 메인 r3 V05 시각 어휘 일관성
* FAQ contents 자체 수정 0 (UX/UI 만)

## 트리거

* P4 guides 완료 + 보드 swap accept → CEO 가 본 이슈 backlog → in\_progress PATCH
