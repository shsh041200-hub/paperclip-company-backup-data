---
name: "PACAA-12 — CTO 재채용 (ONBOARDING.md 첫 프로덕션 검증)"
assignee: "ceo"
---

Phase 2 첫 재채용. PACAA-11 [`templates/agent/ONBOARDING.md`](/PACAA/issues/PACAA-11) 의 첫 프로덕션 검증 겸용.

## 범위

- ONBOARDING.md Phase 0 (의사결정) → Phase 1 (보드 승인 요청) → Phase 2 (에이전트 생성) → Phase 3 (인스트럭션 설치) → Phase 4 (스킬 동기화) → Phase 5 (스모크 하트비트) 풀 사이클 1회 실행
- 12항목 실패모드 체크리스트 통과까지
- 발견되는 갭은 `ONBOARDING.md` 직접 패치 후 잔여 8 직무 일괄 재채용으로 진행

## 의존성

- **PACAA-7 Phase 0**: 기존 CTO 에이전트(`37b7b8bb-8aae-41a4-ae3f-8fc9aeead6e8`) 삭제 필요. [approval 6b6a9300](/PACAA/approvals/6b6a9300-8323-4c30-a68c-957fc0757523) 보드 승인 완료, 보드 콘솔 직접 실행 대기 중. Phase 0 미완료 시 새 CTO 생성 (runbook Phase 2) 차단.
- 본 이슈 Phase 1 (hire proposal + 보드 승인 요청) 은 Phase 0 미완료 상태에서도 작성/제출 가능.

## 산출물 / DoD

- 새 CTO 에이전트 생성 + 인스트럭션/스킬 동기화 완료
- 12항목 실패모드 체크리스트 모두 통과
- 두 번의 연속 실제 작업 하트비트가 체크리스트를 통과 → 본 이슈 done
- ONBOARDING.md 갭 패치 완료 (있다면)

## 모델 / 설정

- `model`: `claude-sonnet-4-6` (보드 디렉티브: CEO 외 Sonnet 기본; 데모된 Sonnet 실패 사례 없음)
- `effort`: `medium`
- `reportsTo`: CEO (`e33ecade-45dc-47ea-9d46-78ef72e8831c`)
- `desiredSkills`: 공통 7 + `paperclip-create-plugin` + `cto-playbook`
