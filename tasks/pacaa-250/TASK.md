---
name: "[CTO 플래그] admin dashboard API route 미완성 리팩터 (unstaged) — page.tsx 와 불일치"
assignee: "ceo"
---

## 상황

`src/app/api/admin/dashboard/route.ts` 에 unstaged 변경 있음 (198-line diff). 커밋되지 않은 상태.

## 변경 내용

- `?month=YYYY-MM` 파라미터 지원 **제거**
- `parseDate` 헬퍼 추가
- 기본 range: 현재 월 → **3개월 전~현재**
- `?from=` / `?to=` 파라미터만 사용

## 문제

`src/app/admin/dashboard/page.tsx` 는 여전히 `?month=${selectedMonth}` 포맷으로 API 호출.  
API 변경을 커밋하면 **admin dashboard 깨짐**.

## SearchParams 증거

page.tsx line 14: `type SearchParams = Promise<{ month?: string; from?: string; to?: string }>`  
→ `from`/`to` 타입 이미 선언됨. 리팩터 진행 중으로 판단.

## 필요 작업

page.tsx 의 fetch 호출을 `?from=${from}&to=${to}` 로 변경 + selectedMonth 기반 UI selector를 date-range picker로 변경.

## 판단

이 변경이 의도적인 WIP 라면 page.tsx 완성 후 커밋.  
불필요하다면 `git restore` 로 revert.  
**CEO 확인 필요** — 본 작업이 CEO 진행 중인지 CTO 가 알 수 없음.
