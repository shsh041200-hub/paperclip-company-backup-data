---
name: "event-driven-orchestration"
description: "Required deadline-discipline protocol for every Packlinx agent. Before setting any time-based deadline on a task, classify it as Category A (externally time-bound) or Category B (event-bound) and convert Category B to event triggers. Used at task creation, plan authoring, and during stall reflection."
slug: "event-driven-orchestration"
metadata:
  paperclip:
    slug: "event-driven-orchestration"
    skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
  paperclipSkillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
  skillKey: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
key: "company/d5e183da-c58f-4124-8075-493330dce4c4/event-driven-orchestration"
---

# Event-driven Orchestration — Packlinx 운영 패러다임

Packlinx는 **AI 에이전트 회사**다. 인간 회사의 시간 기반 운영 가정을
그대로 적용하면 작업이 30분 만에 끝나도 시스템이 3일 마감으로 인식해
체인 작업이 1.5시간이 1주일로 늘어난다. 이 스킬은 그 손실을 막기 위한
**deadline 분류 + 트리거 체인** 프로토콜이다.

이 스킬의 권위 출처는 PACAA-146 보드 디렉티브 (2026-05-01)다.

## 언제 이 스킬을 호출하는가

**필수 호출 시점:**

1. 새 task / issue / child issue 생성 시 — `dueAt` 또는 본문 마감일을
   박기 전 자가 질문 통과 의무.
2. plan 문서 작성 시 — Project Goal / phase / milestone 마다 마감
   분류 의무.
3. 보드/유저 메시지를 task 로 변환 시 — "X일 안에" 같은 인간
   표현을 그대로 받아쓰지 말 것.
4. heartbeat stall reflection 시 — 시간 마감으로 잡혀있던 backlog/blocked
   를 카테고리 B 후보로 재분류.
5. 일반 비즈니스 지식을 적용할 때 — "스프린트", "분기 OKR", "주간
   1-on-1" 등 인간 회사 디폴트가 떠오르면 변환 사전 적용.

**스킵 가능:** 단순 routing, ack, 이미 분류·승인된 작업의 후속 단계.

## 자가 질문 (Self-question, 의무)

새 마감을 박기 직전, 한 줄로 답할 것:

> **"이 마감이 진짜 시간에 의존하는가, 아니면 이전 작업/이벤트
> 완료에 의존하는가?"**

후자면 시간 마감 박지 말고 **트리거 조건**으로 정의한다.

## 두 카테고리

### Category A — Time-based justified (시간 마감 정당)

마감을 시간으로 박는 게 정당한 4가지 사유. 그 외는 전부 B.

1. **외부 의존성** — 우리가 통제할 수 없는 외부 시스템의 처리
   지연. 예: Google 인덱싱 12주, Vercel 응답 36시간, GSC 데이터
   재계산 48시간, 카카오/네이버 API quota 갱신.
2. **데이터 축적 필요** — 일정 기간 누적해야 의미가 생기는 측정.
   예: WUV 베이스라인 1주, 월간 사용자 행동, 분기 코호트 리텐션.
3. **외부 약속/이벤트** — 우리가 외부에 commit 한 일정. 예: 분기
   보고, 투자자 미팅, 계약 만기, 법정 신고 기한.
4. **시장 자연 사이클** — 산업 자체의 시간성. 예: 한국 패키징
   성수기 (9~11월), 명절 휴업, 회계연도.

이 4가지에 해당하는 마감은 시간 마감 유지하되, **원칙 4** (마감일
재정의) 적용.

### Category B — Event-based justified (이벤트 마감 정당)

다음 작업 유형의 시간 마감은 **거의 항상 거짓**이다. 트리거로 변환.

* **제작/생산** — 코드 구현, 디자인 산출, 콘텐츠 작성, 문서 작성.
* **검증** — 코드리뷰, QA, 가설 검증, 테스트 실행.
* **의사결정** — ADR 작성, 옵션 비교, 보드 승인 요청.
* **학습/회고** — 회고록, 결정 audit, post-mortem.

이런 작업의 진짜 의존은 "이전 단계 완료" 또는 "결정 인풋 도착"
이다. "3일 안에"는 인간 회사의 캘린더 압박을 흉내낸 것일 뿐이다.

## 4 운영 원칙

### 원칙 1 — 두 카테고리 분리 (위 정의)

작업 정의 시 카테고리 라벨 의무. 본문 또는 주석에 명시.

### 원칙 2 — 자가 질문 의무

위 자가 질문을 통과 못하면 시간 마감 박지 말 것. 통과하면 어떤
A 사유인지 한 줄로 본문에 명시 ("외부 의존: Google indexing
12주").

### 원칙 3 — 트리거 체인 자동화

이벤트 기반 작업 정의 시 다음 3 요소를 본문 / 메타데이터에 박는다:

1. **선행 조건 (Trigger):** 어떤 이벤트가 발생하면 시작하는가.
   * 예: "PACAA-X 가 status=done 으로 전환되면"
   * 예: "보드가 plan revision N 을 accept 하면"
   * 예: "검증 결과 X 지표가 임계값 통과 시"
2. **즉시 실행:** 트리거 발화 시 마감일 대기 없이 active. Paperclip
   에서는 `parentIssueId` 를 정확히 박아 child completion wake 가
   터지게 하거나, blocker→unblock 시 자동 wake 가 터지게 한다.
3. **후행 알림:** 이 작업 완료 시 다음 작업이 자동 시작되도록
   chained issue 또는 routine trigger 를 미리 박는다. 매번 사람이
   수동 wake 하지 않게.

### 원칙 4 — 시간 마감의 의미 재정의

Category A 에서도 시간 마감 = "데드라인" 아닌 **"검토 시점"**:

* 작업이 일찍 끝나면 즉시 다음 단계 진행 (마감일 대기 X).
* 작업이 마감일까지 안 끝나면 그때 재평가 (자동 fail 처리 X).
* `dueAt` 은 _check-in_ 시그널이지 _commit_ 이 아니다.

## 인간 → AI 변환 사전

CEO 와 모든 에이전트가 일반 비즈니스 지식을 적용할 때 다음 변환
의무. 인간 회사 가정이 떠오르면 **AI 에이전트 회사 등가물**로
교체.

| 인간 회사 가정         | AI 에이전트 회사 변환                                       |
| ---------------- | ------------------------------------------------- |
| "스프린트 2주"        | "이벤트 체인 + Category A 항목만 시간 박싱"                   |
| "분기 OKR"         | "Goal 트리 + 이벤트 트리거 + Category A 측정창"              |
| "주간 1-on-1"      | "트리거 발화 시 자동 보고 / 변경 시 push"                     |
| "프로젝트 간트 차트"     | "이벤트 의존성 그래프 (DAG)"                               |
| "리소스 계획"         | "에이전트 동시성 + 병렬 child issue"                       |
| "마감일 압박"         | "이전 작업 완료 압박"                                     |
| "데일리 스탠드업"       | "heartbeat stall reflection + active child scan"  |
| "분기 리뷰"          | "Category A 측정창 종료 시 자동 회고 트리거"                   |
| "off-site 워크샵"   | "보드 정렬 회의 + 메모 capture (event)"                   |
| "롤아웃 스케줄"        | "feature flag + 카나리 + 메트릭 게이트"                    |
| "에스컬레이션 SLA 4시간" | "blocker 발생 즉시 escalate, hop count 제한"            |

원래 인간 회사에서 통하던 디폴트는 **모두 의심**하라. 95% 는 캘린더
압박 흉내, 5% 만 진짜 시간 의존이다.

## Paperclip 적용 패턴

이 스킬을 Paperclip 위에서 실제 박는 방법:

1. **issue 본문 헤더에 카테고리 명시.** 예:

   ```text
   ## 마감 분류
   - Category: B (제작 작업)
   - Trigger: PACAA-95 status=done
   - 후행: PACAA-104 자동 wake (parentIssueId 세팅)
   ```

2. **`dueAt` 사용 규칙.** Category A 만 `dueAt` 세팅. Category B 는
   `dueAt` 비우고 본문에 트리거 조건 명시.

3. **`parentIssueId` 의무.** child issue 생성 시 항상 세팅. 그래야
   `issue_children_completed` wake 가 자동 발사된다.

4. **Category B 인데 dueAt 박혀있는 issue 발견 시** — stall
   reflection 단계에서 dueAt 제거 + 트리거 명시 PATCH. 보드 승인
   불필요 (작업 의도 변경 아닌 운영 정정).

5. **Category A 에서도 일찍 끝났으면 즉시 다음 단계** — `dueAt`
   까지 대기 금지. 다음 작업의 trigger 조건을 "PACAA-X done" 으로
   박았다면 done 즉시 발사된다.

## Anti-patterns

* **"3일 안에 X" 같은 인간 표현을 그대로 받아쓰기.** 보드/유저가
  그 표현을 써도, 변환 의무는 에이전트에게 있다. "이 마감이 진짜
  시간 의존인가?" 자가 질문 후 답.
* **dueAt 만 박고 trigger 안 적기.** Category A 도 trigger 가 있을
  수 있다 (예: "GSC 데이터 reprocessing 완료 후 측정"). 둘 다 명시.
* **이벤트 작업을 캘린더로 페이싱.** "diff 가 작아도 일주일은
  돌리자" 같은 인간 sprint 디폴트는 AI 에이전트한테는 순손실이다.
* **트리거 체인을 사람이 수동 발사.** 매번 보드가 wake 누르게
  만들지 말 것. parentIssueId / blockedByIssueIds 로 자동화.
* **Category A 사유를 발명.** 진짜 외부 의존이 아니면서 "외부
  의존" 라벨로 시간 박싱 정당화. 4 사유 중 어디에도 안 맞으면
  B 다.

## Self-check (마감 박기 직전)

- [ ] 자가 질문 답함: 시간 의존 / 이벤트 의존
- [ ] Category 라벨 본문에 명시
- [ ] B 면 trigger 조건 + 후행 알림 박음, dueAt 비움
- [ ] A 면 4 사유 중 어느 것인지 명시, dueAt 은 _검토 시점_
- [ ] parentIssueId / blockedByIssueIds 로 자동 wake 체인 구성
- [ ] 인간 회사 가정 (스프린트, 분기, SLA) 사용 시 변환 사전 적용

## 검증 지표 (PACAA-146 보드 합의)

이 스킬 적용 후 1주 측정:

* 작업 평균 완료 시간 (시간 → 시간 단위 기대)
* 체인 작업 (A → B → C) 총 소요 (1주 → 시간 기대)
* 에이전트 idle 시간 (대기 → 즉시 실행 기대)
* `dueAt` 이 박힌 issue 중 Category A 비율 (≥80% 목표)

지표 미달 시 스킬을 보강한다 (anti-pattern 추가, 변환 사전 확장).
