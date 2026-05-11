---
name: "S2 — /compare GSC URL 재색인 요청 (CEO claude-in-chrome 직접)"
assignee: "ceo"
---

## 배경

PACAA-573 C1 compare V05 swap 머지 (PR #82, 2026-05-11). 보드 directive (PACAA-573 코멘트 `dc272aad`): GSC 재제출은 CEO 가 Chrome 직접 열어 처리. 보드 클릭 위임 금지.

## 목표

Google Search Console 에 `https://packlinx.com/compare` 및 대표 `/compare/{slug-A}-vs-{slug-B}` URL 수동 색인 요청 → 재크롤 단축 (며칠~수주 → 1~3일).

## 작업 순서

1. claude-in-chrome `tabs_context_mcp` 로 보드 기존 Chrome 세션 GSC 로그인 상태 확인
2. `https://search.google.com/search-console` 접근 → packlinx.com property 진입
3. 상단 URL 검사 박스에 `/compare` 입력 → "색인 요청" 클릭
4. 추가 대표 1~2개 (`/compare/{popular-slug}-vs-{slug}`) 도 동일 처리
5. 결과 스크린샷 또는 console 로그 본 이슈에 첨부

## Fallback

- 보드 GSC 세션 만료 / property 권한 없음 → 즉시 보드에 1-스텝 가이드 + Before/After 신호 제공 (memory: feedback_external_ui_screenshot_or_pivot)
- agent 직접 시도 1회로 충분, v2 정교화 금지

## Acceptance

- [ ] `/compare` 색인 요청 제출 확인
- [ ] 결과 캡처 본 이슈 코멘트 첨부
- [ ] 보드 개입 0회 (fallback 시만 surface)
