---
name: "[버그] /guides/* Plausible pageview 이벤트 누락 — SPA 라우터 미연동"
assignee: "cto"
---

## 문제

`/guides/*` 경로 페이지에서 Plausible pageview 이벤트가 기록되지 않음.

- `window.plausible` 함수는 탑재 확인됨
- GSC에서 13 클릭 기록(연포장재 가이드) 대비 Plausible 기록 0건
- 원인 추정: Next.js SPA 라우터 전환 시 Plausible 자동 pageview 이벤트 미발동

## 재현 경로

1. https://packlinx.com/guides/flexible-packaging-guide 방문
2. Plausible 대시보드 → Top Pages 확인
3. `/guides/flexible-packaging-guide` 없음

## 요청 사항

- Next.js router 이벤트와 Plausible `pageview` 수동 트리거 연결 확인 및 수정
- 수정 후 Plausible Top Pages에 `/guides/*` 경로 노출 확인

## 관련

- soak 리뷰: [PACAA-187](/PACAA/issues/PACAA-187)
- 원본 가이드 이슈: [PACAA-185](/PACAA/issues/PACAA-185)
