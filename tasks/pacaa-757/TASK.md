---
name: "[FE] V1 디자인 → /companies/[slug] promote — 카카오 섹션 제거 후 적용"
assignee: "frontend-engineer"
---

**부모**: PACAA-755 (보드 결재 완료: 카카오 제거 후 promote).

## 보드 결정 (interaction 6ecb4de3 answered 2026-05-16T11:16:13)
- 카카오 처리 = **A. 제거** (V1 코드 3곳 삭제)
- promote rollout = CEO default **옵션 1 즉시 promote** (보드 stale ask 122e0410 미응답, 회복 인프라 라이브 + Legal risk 제거로 default 진행. 보드가 A/B 또는 보류 원하면 코멘트로 override).

## Scope
### 1. V1 코드 카카오 섹션 제거
`/internal/vendor-redesign/v1/[slug]/page.tsx` (workspace 3177894b/site/app/internal/vendor-redesign/v1/[slug]/page.tsx) 에서 3곳 모두 삭제:
- line ~470-475 + 477-489: 메인 contact card "견적·문의 채널" 의 카카오 노란 버튼 + "Packlinx 운영팀이 해당 업체와 연결" 카피
- line ~529-542: 연락처 0건 vendor fallback "Packlinx 카카오채널로 문의하기"
- line ~594-605: Mobile sticky CTA 카카오 버튼

대안 UX: vendor 의 phone/email/website 만 노출. 셋 다 없으면 "연락처 정보가 등록되지 않았습니다" 만 (CTA 없음).

### 2. V1 → `/companies/[slug]` promote
`/companies/[slug]/page.tsx` 의 현재 디자인을 V1 구조로 교체. 2767 vendor 일괄 적용. 분류 라벨 (vendor_telesales_checks found/not_found) 노출 포함.

대안 구현 (FE 판단):
- A. `/internal/vendor-redesign/v1/[slug]/page.tsx` 의 page 컴포넌트 logic 을 `/companies/[slug]/page.tsx` 로 이식
- B. V1 layout 컴포넌트 추출 → `app/components/vendor-detail/V1Layout.tsx`, 두 라우트 모두 사용 (preview 라우트는 그대로 유지)
- 선호: B (refactor, preview 보존)

### 3. metadata + indexin
