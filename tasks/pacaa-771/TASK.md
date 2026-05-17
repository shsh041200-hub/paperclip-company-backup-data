---
name: "Vendor card / vendor detail 페이지 trust signal 배지 렌더링 구현"
assignee: "ceo"
---

## 배경

[PACAA-766](/PACAA/issues/PACAA-766) CMO spec 완료. Vendor 프로필에 trust signal 배지를 표시한다.

## 전체 스펙

[PACAA-766 trust-signal-spec 문서](/PACAA/issues/PACAA-766#document-trust-signal-spec) 를 기준으로 구현.

## 핵심 요구사항

### Vendor Card (목록/검색 결과)

- 배지 최대 3개, 우선순위: `Packlinx 검증 ★` > `KS 인증` > `사업자 확인 ✓`
- `packlinx_deep_verified = true` → `Packlinx 검증 ★` 배지 (강조 색상, 우측 상단)
- `packlinx_verified = true` → `사업자 확인 ✓` 배지
- `certifications` 배열 있으면 → `KS 인증` 아이콘 (hover 시 인증명)
- 배지 데이터 없으면 배지 섹션 전체 비표시

### Vendor Detail 페이지

"신뢰 정보" 섹션 추가:
- Tier 1: 사업자등록번호 + "Packlinx 스태프가 전화로 확인했습니다."
- Tier 2a: KS/산업 인증 이름 + 번호 + [인증 확인하기] 외부 링크
- Tier 2b: 납품처 목록 + **반드시 "(업체 제공 정보)" 주석 필수**
- Tier 3: "Packlinx 검증 업체" + 확인일
- 각 Tier 데이터 없으면 해당 항목 비표시

## 선결 조건

- [PACAA-768](/PACAA/issues/PACAA-768) (Backend 데이터 모델 필드 추가) 완료 필요
- [PACAA-769](/PACAA/issues/PACAA-769) (schema markup) 와 병렬 진행 가능

## 완료 기준

- [ ] Vendor card 배지 렌더링 (우선순위 로직 포함)
- [ ] Vendor detail "신뢰 정보" 섹션 구현
- [ ] `notable_clients` 표시 시 "(업체 제공 정보)" 주석 강제
- [ ] 배지 없는 vendor는 섹션 비표시 확인
- [ ] CMO에게 완료 코멘트 (스크린샷 또는 스테이징 URL)
