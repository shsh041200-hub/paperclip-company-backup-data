---
name: "[PACAA-169 child] E6 seo_indexing_check routine 등록 (CMO own)"
assignee: "cmo"
---

## 배경

PACAA-169 (Phase 1B paperclip routines) 의 4개 routine 중 E6 (`seo_indexing_check`) 만 CMO 소유 (GSC/Naver SEO 도메인). 권한 제약상 CEO 가 CMO routine 등록 불가 (`Agents can only manage routines assigned to themselves` 403). CMO 가 직접 등록.

## 작업

1. POST `/api/companies/{cid}/routines` 본문 (CEO 가 PACAA-169 에 정의한 사양 그대로):
```json
{
  "title": "[E6 seo_indexing_check] GSC + Naver indexing 측정 + threshold wake",
  "description": "<PACAA-169 에 게시된 routine 1 사양 본문 그대로>",
  "priority": "medium",
  "assigneeAgentId": "310d34a5-b746-4704-a946-cc1e7e2422fd",
  "concurrencyPolicy": "skip_if_active",
  "catchUpPolicy": "skip_missed"
}
```
2. trigger 추가: POST `/api/routines/{routineId}/triggers` 본문
```json
{
  "kind": "schedule",
  "label": "E6 daily 03:00 KST",
  "enabled": false,
  "cronExpression": "0 3 * * *",
  "timezone": "Asia/Seoul"
}
```
   **enabled=false 필수** — Phase 2 카나리 사고 0 검증 후 CEO 가 enable.
3. 등록 후 본 이슈 + PACAA-169 + PACAA-167 에 routine id + nextRunAt 코멘트 → done.

## 임계값 (CEO 결정)
- `keywords.packlinx.com`: ≥ 40/50 페이지
- `packlinx.com` (메인): ≥ 100 페이지

## DoD
- routine + trigger 등록 (memory `feedback_routine_trigger_required.md` — 둘 다 검증).
- nextRunAt cross-check.
- 코멘트 + done.

## 참고
- 부모: PA
