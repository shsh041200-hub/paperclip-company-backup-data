---
name: "보드 대시보드 — \"사장님이 지금 해야 할 일\" 섹션 추가"
assignee: "cto"
---

## 부모 이슈

[PACAA-109](/PACAA/issues/PACAA-109) — 보드 follow-up.

## 보드 요구사항 (원문)

> 추가로 지금 당장 보드가 해야할일도 추가해

## 컨텍스트 — 기존 `보드 액션 큐` 의 한계

현재 `generate-dashboard.py:render_action_queue` 는 `/api/companies/{cid}/approvals?status=pending` 만 본다. 다음을 **누락**:

* 이슈 단위 인터랙션 (`request_confirmation`, `ask_user_questions`) 의 `pending` 상태
* 에이전트 단위 `errored` / `paused with reason` 상태 (사장님 개입 필요할 때)
* `deferred_items.md` 에서 트리거 도래해 능동 알림 큐에 들어간 항목

결과: 라이브 대시보드에서 "보드 액션 큐 — 현재 대기 중인 액션 없음" 이 표시되지만 실제로는 이슈 단위 인터랙션이 여러 건 pending. 보드는 텔레그램으로만 그 사실을 알 수 있어 "한 화면에서 한눈에" 라는 요구를 충족 못함.

## 작업 정의

### 1. 신 섹션 위치 + 헤더

**신 섹션을** [PACAA-110](/PACAA/issues/PACAA-110) **의 `<section class="now-section">` 보다 "위"** (`<h1>` 바로 아래, 가장 먼저 보이는 자리) 에 삽입. 사장님 본인이 해야 할 일 \= 최우선.

헤더 후보 (CTO 재량):

* `사장님이 지금 해야 할 일` (직설적, 일관성)
* `지금 결정/응답해 주세요` (행동 유도)

### 2. 데이터 소스 통합

`render_board_actions(approvals, interactions_by_issue, agents, deferred_items)` 신 함수에서 다음을 모두 끌어옴:

* 결재 대기: `approvals` (기존 데이터 재사용)
* 승인 카드: 이슈별 `interactions` 중 `kind=request_confirmation` + `status=pending`
* 질문 카드: `kind=ask_user_questions` + `status=pending`
* 에이전트 이상: `agents` 중 `status=errored` 또는 `pauseReason` non-null
* 능동 알림 큐: `deferred_i
