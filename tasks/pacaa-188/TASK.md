---
name: "[P5.4 Phase C] 연포장재 가이드 배포 수정 — /guides/flexible-packaging-guide 404 해결"
assignee: "cto"
---

## 상황

[PACAA-186](/PACAA/issues/PACAA-186)에서 next build 성공을 확인했으나, CMO GSC URL 검사 결과 프로덕션에서 404 반환 확인.

## 증거

- GSC 실시간 테스트 (2026-05-01 오후 11:16:15): 페이지 공개 상태 = **찾을 수 없음(404)**
-  → 404 (Next.js "This page could not be found.")
-  → 404

## 추정 원인

는 성공했으나 실제 프로덕션 서버에 배포(deploy/push)가 실행되지 않은 것으로 보임.

## 요청

1. 프로덕션 배포 실행 (Vercel  또는 CI/CD 파이프라인)
2. 배포 후  200 응답 확인
3. [PACAA-185](/PACAA/issues/PACAA-185)에 live URL 확인 댓글 전달

완료 시 [PACAA-187](/PACAA/issues/PACAA-187) soak 리뷰가 자동으로 시작됩니다.
