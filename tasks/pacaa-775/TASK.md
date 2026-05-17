---
name: "[FE] Trust signal 표시 Legal 반영 — packlinx_verified 뱃지 평가기준 링크 + notable_clients 자기신고 라벨"
assignee: "backend-engineer"
---

## 배경

[PACAA-773](/PACAA/issues/PACAA-773) CMO가 작성한 Legal 권고사항 반영 프론트엔드 스펙에 따라 구현이 필요합니다.
전체 스펙: [PACAA-773 spec document](/PACAA/issues/PACAA-773#document-spec)

---

## 구현 항목

### 1. `packlinx_verified` 뱃지 컴포넌트 — 평가기준 링크/아이콘 추가

**변경 내용:**
- Vendor 프로필 페이지의 `packlinx_verified` 뱃지 컴포넌트에 `(ⓘ)` 정보 아이콘 추가
- 아이콘 클릭/호버 시 팝오버(또는 링크) 표시: `"평가기준 보기"` → `/verified-criteria`
- `/verified-criteria` 페이지 미존재 시 뱃지 자체를 숨김 처리 (조건부 렌더 또는 feature flag)
- 뱃지 단독 표시 케이스 제거 (반드시 `(ⓘ)` 병기)

**팝오버 텍스트:**
```
Packlinx 인증은 사업자등록 진위 확인, 통신판매업 신고 확인,
최근 6개월 분쟁 0건 등 내부 검수팀이 확인한 업체에 부여됩니다.
[평가기준 전체 보기 →]
```

### 2. `notable_clients` 섹션 — "자기신고" 라벨 추가

**변경 내용:**
- `notable_clients` 배열이 1개 이상일 때 각 항목 옆 또는 섹션 하단에 라벨 추가
- 라벨 텍스트: `[자기신고]` (짧은 버전) 또는 `본 정보는 vendor 자기신고이며 Packlinx가 검증하지 않았습니다` (긴 버전)
- 색상: 중립 회색 (#6B7280), 최소 폰트 8pt
- 고객사 로고 이미지 렌더링 제거 (텍스트만 노출)
- `notable_clients` null/빈 배열이면 섹션 자체 미표시

---

## Acceptance Criteria

### packlinx_verified 뱃지
- [ ] `packlinx_verified=TRUE` vendor 프로필에서 뱃지가 `(ⓘ)` 아이콘과 함께 렌더링됨
- [ ] `(ⓘ)` 클릭/호버 시 평가기준 팝오버 또는 `/verified-criteria` 링크 노출
- [ ] `/verified-criteria` 페이지 없을 시 뱃지 렌더링 숨김 처리
- [ ] 뱃지 단독 표시 케이스 없음

### notable_clients 라벨
- [ ] 배열 1개 이상 시 `[자기신고]` 배지 또는 섹션 하단 라
