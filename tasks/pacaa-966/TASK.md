---
name: "[CTO] 토큰 효율 — heartbeat 동적 backoff (PACAA-963 T1A)"
assignee: "cto"
---

## 배경

PACAA-963 토큰 사용량 분석 결과 보드 승인 항목 (옵션 t1a). PACAA-963 보드 응답 (interaction 5d097bca) 에서 채택.

## 문제

- 회사 1000 wake / 2.56일 중 67% 가 quick-exit (의미있는 작업 없음).
- CEO 단독으로 회사 토큰의 80% 소비. heartbeat timer 가 그 64%.
- 정적 인터벌 7→15분 (B1, accepted) 은 즉시 효과 있으나 cache TTL 5분 만료 미스 추가 발생 가능.

## Goal — 동적 backoff

- 연속 quick-exit N회 → 다음 timer 인터벌 2x (cap 30분).
- Event wake (issue_assigned / issue_commented / automation) 도착 시 인터벌 reset.
- 효과: 작업 활발기 = 짧은 인터벌 유지, idle 기 = 자동 backoff.

## Acceptance

- [ ] paperclipai (또는 adapter layer) 에 backoff 로직 추가
- [ ] CEO + 모든 sub-agent 에 enable, 기본 cap=30분
- [ ] 1주 회귀 메트릭: 평균 quick-exit 비용 30%↓ 또는 wake 빈도 30%↓
- [ ] 보드 응답 SLA 회귀 없음 (issue_commented → wake 즉시성 유지)

## 가역성

config flag 로 disable 가능 설계.

## 측정

`heartbeat-runs/usageJson.rawCachedInputTokens` + `costUsd` per agent 주간 비교.

## 페어 항목 (PACAA-963)

- t2a (A1, MEMORY.md 압축) — PACAA-965, **완료**.
- B1 (CEO intervalSec 15분) — 완료 (`runtimeConfig.heartbeat.intervalSec=900`).
- 본 t1a 가 B1 위에 동적 layer 추가.
