---
name: "PACAA-497 후속 — cert chip 색상 + 메인 메타 title V05 polish"
assignee: "ceo"
---

## 배경

PACAA-497 R3-D CEO 검토에서 지적된 pre-existing 위반 2건 후속 처리.

## 작업 범위

### 1. cert filter chip 색상 토큰화

`app/page.tsx` CERT_CATEGORY_COLORS 객체 (line ~97):
- `bg-blue-500 border-blue-500` → V04 design system 정합 토큰으로 교체
- `bg-green-600 border-green-600` → 동일
- `text-amber-400` (별점) → neutral 또는 제거

PACAA-485 V04 swap 이전 잔존 코드. Lock 규칙: amber/blue/green 전무.

### 2. 메인 페이지 메타 title SEO

현재: `"전국 패키징 업체 찾기 — B2B 포장재 플랫폼 | Packlinx"`
V05 컨셉 정합: `"포장재 파트너 찾기 | Packlinx"` 또는 유사

SEO 임팩트 확인 후 CEO 동의 하에 변경.

## 트리거

PR #55 머지 완료 후 시작.
