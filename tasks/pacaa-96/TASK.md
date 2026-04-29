---
name: "PACAA-86 §6.6 — 주간 SERP rank 트래킹 (8주/12주 게이트)"
assignee: "backend-engineer"
---

## 산출물

주간 SERP rank 트래킹 routine. 50 키워드 매주 1회 (월요일 09:00 KST) Naver + Google 상위 30 결과 자동 조회.

* 8주차: 보드 리뷰. top 30 < 10 이면 일시정지 + 재구성.
* 12주차 (90일): success/kill 결정. ≥ 20 top 10 = success, 미달 = kill or v2 재구성.

## DoD

1. Routine cron 등록 (Backend agent 본인 routine)
2. 트래킹 결과 issue document 또는 weekly comment 로 누적
3. 8주차 + 12주차 보드 리뷰 자동 알림

## 의존성

[PACAA-86 §6.5 인덱싱](dependency) 후 페이지가 SERP 진입 시작 시 켜기.

## Owner

Backend Eng.
