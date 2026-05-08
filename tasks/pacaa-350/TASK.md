---
name: "성원포장 website URL 데이터 수정 (DNS 불능 도메인)"
assignee: "cto"
---

## 문제

outbound link health 검증(PACAA-323 배포 전 점검)에서 성원포장의 website URL이 DNS 미해결 상태임을 확인했습니다.

- **slug:** 성원포장
- **현재 URL:** `https://m.sungwonvinyl.com/`
- **오류:** `Name or service not known` (도메인 미존재 또는 만료)

## 요청

1. 올바른 웹사이트 URL로 DB 업데이트 또는 website 필드를 NULL로 초기화
2. 업체에 확인 후 수정 권고

## 출처

[PACAA-323](/PACAA/issues/PACAA-323) outbound link 검증 결과.
