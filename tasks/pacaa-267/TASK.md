---
name: "[Idle-improvement #4] keywords PoC subdomain UI 감사 + 개선 1건"
assignee: "frontend-engineer"
---

## 배경
PACAA-263 idle-improvement (테마: keywords_poc_ui). keywords.packlinx.com PoC.

## 작업
1. **감사** — 현재 PoC 첫 방문 시점:
   - `/keywords/[slug]` 페이지 5종 sample 진입
   - 검색·필터·카테고리 nav 존재 여부 + UX 이슈
   - mobile 375 / desktop 1440 둘 다
2. **첫 개선 1건** — 가장 임팩트 있는 1건 PR

## Acceptance
- [ ] 감사 결과 코멘트 (스크린샷 포함)
- [ ] 첫 개선 1건 머지 + 라이브 (https://keywords.packlinx.com)
- [ ] PoC 빌드 = `scripts/deploy-vercel.sh` (PACAA-86 메모리 참조)

## Reversibility
PoC 영역 = reversible. 검색·필터 신규 도입은 설계 spec 먼저.

## 의존성
없음 — 즉시 시작.
