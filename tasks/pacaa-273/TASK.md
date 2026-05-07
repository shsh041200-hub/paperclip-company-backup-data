---
name: "[긴급] 사이트맵 plastic-containers-guide 404 제거"
assignee: "cto"
---

## 배경

[PACAA-269](/PACAA/issues/PACAA-269) 감사 중 발견. 사이트맵()에 404를 반환하는 URL이 포함되어 있음.

## 문제

 → HTTP 404

사이트맵에 404 URL이 포함되면 GSC Coverage error로 분류됨. 도메인 전체 신뢰도에 영향.

## 작업

 생성 로직에서  항목 제거.

확인: 제거 후  Google 검색 시 결과 없음 확인.

## Acceptance
- [ ] 사이트맵에서 plastic-containers-guide URL 제거
- [ ] 배포 후 sitemap.xml에서 해당 URL 없음 확인

## Reversibility

사이트맵 항목 제거 = 저위험. 404 URL은 어차피 Google이 이미 오류로 처리 중.
