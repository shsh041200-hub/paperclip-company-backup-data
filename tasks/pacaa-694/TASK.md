---
name: "[CEO] sub-agent skill baking — CEO 결정 vs 보드 결정 라우팅 룰"
assignee: "ceo"
---

## 배경

12h 안에 sub-agent (BE/FE) 가 `request_confirmation` 또는 `ask_user_questions` 로 CEO 결정 (PR 머지·데이터 마이그레이션·옵션 선택) 요청한 사례 4건, 인터랙션 5건:

- PACAA-681 FE `9ee429fa` (PR #107 머지)
- PACAA-682 BE `cc848d09` (Step 3+4 마이그레이션)
- PACAA-688 BE `d688ee4a` (90% chase 옵션)
- PACAA-691 BE `f9d48301` + `542fc416` + `816e72b1` (dedup GROUP A/B)

각 케이스마다 CEO 가 코멘트 sign-off + 패턴 정정 코멘트로 close.

## 문제

- `request_confirmation` accept/respond = 보드 전용 (CEO 는 401), 따라서 sub-agent 발의 시 보드 텔레그램 미스라우팅.
- 인터랙션 DELETE 엔드포인트 없음 → 영구 stale.
- 메모리 entry [[feedback_subagent_pr_merge_routing]] (CEO 만 가짐) 으로는 sub-agent 행동 변경 안 됨.

## 작업 범위

1. **BE/FE 의 `instructionsFilePath` 또는 공통 skill (e.g. `packlinx-comms`) 에 룰 baking:**
   - "CEO 결정 (가역 ops/data/PR 머지/옵션 선택) 요청 = 코멘트 escalation 만"
   - "보드 결정 (자금·policy·one-way door·외부 자원) 요청 = `request_confirmation` 또는 `ask_user_questions`"
   - 트리거 phrase 예시 + 잘못된 vs 올바른 패턴 비교 포함
2. 가능하면 CMO/Legal Counsel/general 에이전트도 동일 룰 baking (cross-agent 동질화).
3. 적용 후 다음 sub-agent ticket 1~2 wake 관찰 → 회귀 확인.

## DoD

- 룰이 sub-agent skill 또는 instructions 파일에 명시되어 라이브.
- 적용 후 CEO 결정 ticket 에서 sub-agent 가 코멘트 escalation 만 사용 (interaction 0).

## 게이트

CEO 단독 (내부 agent 운영 설정, 보드 승인 불요).

##
