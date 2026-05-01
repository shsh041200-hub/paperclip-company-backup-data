---
name: "[PACAA-146 mid-term] Plan v3 Project Goal A/B 재라벨 + 의존성 그래프 재구성"
assignee: "ceo"
---

## 마감 분류
- Category: B (의사결정 + 학습 작업)
- Trigger: 보드가 PACAA-146 의 request_confirmation 을 accept 하면 즉시 시작
- 후행: 재구성된 plan v3 → 보드 accept → 모든 산하 child issue 의 dueAt/trigger 일괄 PATCH
- dueAt 비움 (Category B). 1주 측정창은 PACAA-146 검증 routine 이 별도로 측정

## 작업 내용 (PACAA-146 mid-term 단계)

1. plan v3 의 모든 Project Goal / phase / milestone 스캔
2. 각각 A/B 라벨 부여 (event-driven-orchestration skill 의 4 사유 기준)
3. B 항목의 시간 마감 → 트리거 조건으로 변환
   - "Pair 2 SG-X 통과 시" / "이전 milestone done 시" / "메트릭 게이트 통과 시" 등 명시
4. 의존성 그래프 재구성 (시간축 → 이벤트 DAG)
5. 변환된 plan v3 revision 작성 → 보드에 request_confirmation
6. accept 후 산하 child issue 의 dueAt PATCH (B 는 비우고 trigger 본문에 명시)

## 수용 기준

* plan v3 의 모든 Goal/phase/milestone 에 A/B 라벨
* B 항목 중 dueAt 박혀있는 것 0건
* A 항목은 4 사유 중 어느 것인지 본문 명시
* 의존성 그래프 (Mermaid 또는 list) 가 plan 문서에 포함

## 시작 조건

PACAA-146 의 request_confirmation 이 보드에 의해 accept 되면 즉시 시작.
이 issue 는 그때까지 backlog (외부 대기, 합법) — accept wake 시 in_progress 전환.
