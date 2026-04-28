---
name: "SG-3 측정 인프라 사전 준비 (Plausible 셋업 + 의존성 + 1주차 계획)"
assignee: "cto"
---

## 배경

PACAA-25 plan v3 보드 사인오프 완료 (2026-04-28). 카테고리 후보 리스트
([PACAA-26](/PACAA/issues/PACAA-26)) 사인오프 대기 중 SG-3 워밍업
진행을 위한 사전 준비 티켓.

## 목적

카테고리 사인오프가 떨어지자마자 SG-3(P3.1~P3.5)을 즉시 작업 시작
가능하도록 인프라/계획 사전 준비.

## 작업 범위

다음 3가지를 이슈 plan 문서에 정리:

### 1. Plausible 계정 셋업 가능 여부 확인

- Plausible Cloud 계정 생성 가능성 (결제 카드, 도메인 verification)
- self-hosted Plausible 옵션과 비교
- 한국 IP only 필터링 적용 가능 여부 (custom segment 또는 별도
  property 분리)
- bot UA 제외 + admin/사무실 IP 제외 메커니즘
- 비용 (Cloud ~$9/mo vs self-host) 추천

### 2. P3.1~P3.5 의존성 파악

P3.1 (정보 수정 요청 UI + counter), P3.2 (paid intent 폼), P3.3
(self-registration 폼 + 태깅), P3.4 (검색 행동 + WUV 대시보드), P3.5
(주간 자동 리포트)에 대해:

- 어느 것이 병렬 가능한가 (DB schema 충돌 / UI 컴포넌트 충돌 없음)
- 어느 것이 직렬 종속인가 (P3.1~3.4 결과를 P3.5가 모음)
- packlinx.com 코드베이스에서 각 작업의 작업 영역 (어떤 라우트, 어떤
  컴포넌트, 어떤 DB 테이블)
- 추정 작업 시간 (현재 1~2주 명목치 검증)

### 3. 사인오프 직후 첫 1주 작업 계획 초안

- Day 0~1: Plausible 셋업 + custom event 정의 + 기본 dashboard
- Day 2~5: P3.1, P3.2, P3.3 병렬 시작 (가능 시)
- Day 6~7: 첫 데이터 검증 + P3.4 시작
- 어떤 PR / 커밋이 1주차에 머지될지 구체 명시

## 산출물

이 이슈의 plan 문서에 위 3개 섹션 정리. CEO에게 review 요청.

## 시한

1주 (이 이슈 자체. 계획 작업이지 구현 작업 아님)

## 의존성

없음. 카테고리 후보 리스트(PACAA-26) 사인오프와 독립적으로 진행 가능.

## Owner

CTO 단독.
