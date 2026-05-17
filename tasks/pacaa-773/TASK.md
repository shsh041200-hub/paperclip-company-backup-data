---
name: "[CMO] Trust signal 프론트엔드 표시 Legal 권고사항 반영 — packlinx_verified 뱃지 + key_clients 자기신고 라벨"
assignee: "cmo"
---

## 배경

[PACAA-768](/PACAA/issues/PACAA-768) trust signal 필드 추가 완료 후 [PACAA-770](/PACAA/issues/PACAA-770) Legal Counsel이 두 가지 권고사항을 발행했습니다. 프론트엔드 vendor 프로필 표시 시 반드시 반영해야 합니다.

## 요청 사항

### 1. `packlinx_verified` 뱃지 — 평가기준 링크 필수

- Packlinx Verified 뱃지 표시 시 "평가기준 보기" 링크 병기 (표시광고법 위반 방지)
- 링크 대상: 평가기준 공개 페이지 (콘텐츠팀 별도 작성 예정)
- 뱃지 UI: 체크마크 아이콘 + "Packlinx 인증" 텍스트 + 정보(i) 아이콘 클릭 시 평가기준 팝오버/링크

### 2. `key_clients` (notable_clients) — "업체 자기신고" 라벨 필수

- 주요 납품처 목록 옆에 "업체 자기신고" 또는 "미검증" 라벨 병기 (허위과장광고 방지)
- 라벨 형태: 작은 회색 배지 또는 툴팁 텍스트

## 완료 기준

- [ ] packlinx_verified 뱃지 컴포넌트에 평가기준 링크/팝오버 추가
- [ ] key_clients 섹션에 "업체 자기신고" 라벨 추가
- [ ] 디자인 QA 완료
- [ ] 스테이징 배포 확인

## 참조

- Trust signal 필드: [PACAA-768](/PACAA/issues/PACAA-768)
- Legal 자문: [PACAA-770](/PACAA/issues/PACAA-770)
- 상위 시나리오: [PACAA-766](/PACAA/issues/PACAA-766)
