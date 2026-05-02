---
name: "E5 Worker: Paperclip wake-comment 권한 제약 해소 (Complete Mediation bypass)"
assignee: "ceo"
---

## 배경

[PACAA-168](/PACAA/issues/PACAA-168) 배포 중 발견. E5 Worker service-account agent(`6fb76456`)가 다른 에이전트에 **할당된** 이슈에 코멘트를 게시할 수 없음.

Paperclip의 Complete Mediation 정책: `"Agent cannot mutate another agent's issue"`

## 영향

실제 wake 대상 이슈는 대부분 특정 에이전트에 할당되어 있음. 현재 E5 Worker는 **미할당 이슈에만** wake 코멘트 전송 가능 → wake 메커니즘이 사실상 작동하지 않음.

## 필요 결정

CEO/CTO가 Paperclip에 다음 중 하나를 추가해야 함:

1. **Option A**: 특정 agent role (`wake-poster`) 에게 cross-agent comment 허용
2. **Option B**: `POST /api/issues/{id}/comments` 에 `bypassAssignmentCheck: true` 플래그 (API-key 스코프 제한)
3. **Option C**: E5 Worker를 CEO agent 가장으로 실행 (PAPERCLIP_API_KEY = CEO JWT)

**추천**: Option A — 최소 권한 원칙 유지.

## 우선순위

현재 E5 Worker는 배포 완료되었으나 실제 wake 기능이 무력화된 상태. Phase 2 카나리 전에 해결 필요.
