---
name: "[FE] PACAA-529 vendor profile 페이지 박탈 배너 구현 (LC §5-B 통지)"
assignee: "frontend-engineer"
---

## 목적

[PACAA-529](/PACAA/issues/PACAA-529) 보드 사인오프 완료 (2026-05-11T03:17 KST). Legal Counsel §5-B 통지 의무 이행을 위해 revoked vendor 공개 profile 페이지에 배너를 게시한다.

## 배경

- 대상 vendor: 20개 (`is_verified=false AND verification_revoked_reason='audit_2026Q2_evidence_missing'`)
- LC 채널 결정: 공개 `/vendor/{slug}` 페이지 상단 배너 (이메일 대체 — 20개 업체 전원 이메일 없음)
- 법적 근거: [PACAA-530](/PACAA/issues/PACAA-530) LC §5-B 자문 — 조건부 적합 (리스크: 낮음)

## 승인된 배너 카피 (변경 금지)

```
[공지] is_verified 배지 상태 변경 안내

귀사 프로필의 인증 배지가 2026년 5월 11일부로 비표시 처리되었습니다.
사유: 2026-Q2 감사 결과 §1 검증 기준 evidence(사업자등록번호·도메인·이메일·전화·양방향 연락처) 미확인.
기준 전문 → https://packlinx.com/docs/legal/vendor-verification-criteria
보완 기간: 2026-05-11 ~ 2026-08-09 (90일) 내 evidence 제출 시 배지 복구 절차 진행.
제출: verify@packlinx.com | 문의: contact@packlinx.com
```

## LC 필수 조건 (5가지 — 모두 충족 필수)

1. **위치**: `/vendor/{slug}` 페이지 최상단 (hero/헤더 바로 아래). 푸터·접힘 영역 불가. 시각적 prominence 필수.
2. **본문**: 위 카피 원문 그대로 (§5-B 3요건: 박탈 사실·사유·90일 grace+복구채널 전부 포함)
3. **조건부 렌더링**: `is_verified=false AND verification_revoked_reason='audit_2026Q2_evidence_missing'` 인 vendor 페이지에만 표시 (현재 20개)
4. **Server-log**: 배너 최초 렌더링 시각 per vendor (SSR 기준) — LC 의무 이행 입증 자료
5. **유지 기간**: 2026-08-09까지 상시 표시. `verification_revoked
