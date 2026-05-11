---
name: "PACAA-490 P0 hotfix — preview false claim 즉시 삭제 + v3 카피 swap + PR #52 close"
assignee: "frontend-engineer"
---

## Context

부모: PACAA-490 (사이트 전체 ux/ui 개선). 보드 directive (PACAA-493 c7899cf9, 2026-05-11 KST):

> 사업자등록번호 검증된 업체 포함 이문구는 삭제해 우리 웹사이트는 사업자등록번호를 검증하는 로직은 없어

false claim — 표시광고법성. production 에는 이미 없음 (라이브 grep 확인). preview-only (v1/v2/v3, noindex). r3 round 진행 중 보드가 v1/v2/v3 preview 다시 열어볼 위험 있어 즉시 삭제.

동시에 보드의 v3 카피 swap directive도 적용 (v3 가 r3 round 에서 살아남을 수도, deprecate 될 수도 있으나 lock-set 일관성 측면에서 즉시 적용).

## 작업 범위 (단일 PR, base=main)

### 1. False claim 삭제 (필수, 3 라인)

- `app/design-preview/main-r2-v1/page.tsx:90` — "사업자등록번호 검증된 업체 포함. 식품·이커머스·화장품·의약·전자 전 분야." → 뒷 문장만 남기거나 삭제 (CMO 톤 유지)
- `app/design-preview/main-r2-v2/page.tsx:156` — "사업자등록번호 검증된 업체 포함. 공개된 출처에서 자동 수집 후 확인." → "공개된 출처에서 자동 수집 후 확인." 만 유지
- `app/design-preview/main-r2-v3/MainR2V3Client.tsx:258` — "사업자등록번호 검증된 업체 포함 · <span ...>1,380개</span> 등록" → "<span>1,380개</span> 등록" 만 유지

### 2. v3 카피 swap (1 라인)

- `app/design-preview/main-r2-v3/MainR2V3Client.tsx:241` — "패키징 업체 디렉토리" → "패키징 업체 검색 플랫폼"

### 3. PR #52 close + branch 삭제

- 본 hotfix PR open 전 또는 후, GitHub UI 또는 gh CLI 로 PR #52 close (머지 안 함). branch `feat/PACAA-493-v3-polish-guide-separation` 삭제 (잔여 0).

## Lock 유지

- production /app/page.tsx 변경 0
- 다른 design-pre
