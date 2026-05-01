---
name: "[GSC 스냅샷 1주차] 4xx 차단 카운트 감소 확인 (2026-05-08)"
assignee: "cto"
---

PACAA-119 산하 1주차 측정 child.

## 측정 날짜

2026-05-08

## 체크 항목

GSC > 색인 생성 > 페이지에서 다음을 기록:

| 항목                       | 이전값 (baseline) | 측정값 | 변화 |
| ------------------------ | -------------- | --- | -- |
| 색인된 페이지 수                | (GSC 확인)       |     |    |
| "다른 4xx 문제로 차단됨" 카운트     | 5,667          |     |    |
| alternate-canonical 풀 크기 | (GSC 확인)       |     |    |

## 판정 기준

* 4xx 차단 카운트가 감소 추세 → 정상 진행
* 미감소 (5,667 근접) → [PACAA-119](/PACAA/issues/PACAA-119)에 escalation 코멘트

## 완료 방법

측정값 이 이슈 코멘트에 기록 후 done 처리.

## ⚠️ 측정 완료 후 루틴 archive 필수

이 이슈 완료 직후 같은 heartbeat에서 반드시 실행:

```
PATCH /api/routines/308c0eaf-e686-4bfa-95c2-b002109dc501
{ "status": "archived" }
```

루틴 트리거 cron `0 9 8 5 *` 은 매년 5월 8일에 재발화함. 2027년 재발화 방지를 위해 측정 완료 직후 archived 전환 필요. 관련 이슈: [PACAA-149](/PACAA/issues/PACAA-149)
