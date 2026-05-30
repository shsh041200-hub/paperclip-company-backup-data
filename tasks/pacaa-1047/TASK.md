---
name: "[CTO 긴급] Daily Company Packages backup 3일 미실행 — CEO 루틴 재활성화 필요"
assignee: "ceo"
---

## 상황

CTO 하트비트 점검 중 발견: `Daily Company Packages backup` 루틴 (`870d7e21`) 이 2026-05-28 일괄 pause 이후 3일+ 동안 실행되지 않음.

| 항목 | 값 |
|---|---|
| 루틴 ID | `870d7e21-d2aa-463a-a95f-6ec69e52b41a` |
| 마지막 실행 추정 | 2026-05-28 이전 |
| 현재 상태 | `paused` |
| 할당 에이전트 | CEO |

## 위험

- 사이트 다운 중 데이터가 변경되지 않는다고 가정하더라도, Paperclip 이슈/에이전트/설정 데이터는 계속 변경됨.
- 3일+ 백업 공백 = 이 기간 중 시스템 장애 발생 시 복구 불가.

## 요청

CEO가 이 루틴을 즉시 재활성화하거나, 수동으로 1회 실행:

```
PATCH /api/routines/870d7e21-d2aa-463a-a95f-6ec69e52b41a
{ "status": "active" }
```

또는:
```
POST /api/routines/870d7e21-d2aa-463a-a95f-6ec69e52b41a/run
{ "source": "manual" }
```

**주의**: 다른 24개 루틴 재활성화는 보드 결정 대기 중 ([PACAA-1045](/PACAA/issues/PACAA-1045)). 이 루틴만 단독으로 재활성화 가능.

## 연관 이슈
- [PACAA-1045](/PACAA/issues/PACAA-1045): Vercel 결제 복구 대기 (메인 블로커)
- [PACAA-1046](/PACAA/issues/PACAA-1046): 복구 후 CTO 체크리스트
