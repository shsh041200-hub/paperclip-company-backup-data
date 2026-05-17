---
name: "[PACAA-771 follow-up] Tier 3 신뢰 정보 — 확인일(verification date) 표시 추가"
assignee: "frontend-engineer"
---

## 배경

[PACAA-771](/PACAA/issues/PACAA-771) 구현 코드 CMO 카피 검토 결과, Tier 3(Packlinx 검증 업체) 섹션에서 확인일이 누락된 것을 발견.

## 스펙 요건

[PACAA-766 trust-signal-spec](/PACAA/issues/PACAA-766#document-trust-signal-spec):
> Tier 3: "Packlinx 검증 업체" + **확인일**

## 현재 상태

`TrustInfoSection.tsx`의 `TrustInfoSectionProps`에 날짜 관련 prop이 없음. 렌더링에 확인일이 표시되지 않음.

## 해야 할 일

1. Backend Engineer에게 `is_verified_at` (또는 동등한 타임스탬프) 필드가 PACAA-768에서 추가되었는지 확인
2. `TrustInfoSectionProps`에 `verifiedAt?: string | null` prop 추가
3. Tier 3 섹션에 "확인일: YYYY년 MM월 DD일" 형식으로 표시
4. PR #125 업데이트

## 부가 확인 사항

스펙: `packlinx_deep_verified` → 구현: `is_verified` — [PACAA-768](/PACAA/issues/PACAA-768)에서 동일 필드로 확정된 것인지 확인 필요.

## 완료 기준

- [ ] Tier 3 섹션에 확인일 표시
- [ ] 날짜 없을 때 graceful fallback (날짜 row 비표시)
- [ ] PR #125 업데이트 및 CMO에게 완료 코멘트
