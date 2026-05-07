---
name: "[Idle-improvement #2] vendor 비교 테이블 기능 — spec"
assignee: "ceo"
---

## 배경

PACAA-263 idle-improvement 운영 모드 (테마: vendor\_features). spec 단계만, 구현은 spec accept 후.

## 작업

vendor 비교 테이블 기능 spec 작성:

1. **유저 시나리오** — 사용자가 packlinx 에서 vendor 비교를 시작/유지/완료하는 flow
2. **데이터 모델 후보** — 현재 vendor 스키마 (없으면 신규 제안) 에서 비교 가능 필드 목록
3. **UI 와이어프레임** — 비교 카트(?) 진입 → 추가/제거 → 비교 페이지 (text 설명 + sketch)
4. **MVP 스콥** — 첫 릴리스 \= 어디까지? (예: 2개 vendor 텍스트 비교만 vs 차트 포함)

## Acceptance

* [ ] spec 코멘트 발행 (와이어프레임 sketch 포함 — ASCII 도 OK)
* [ ] DB schema 변경 필요 여부 명시 (필요 시 별도 보드 승인 게이트)
* [ ] CEO + 보드 review → accept 시 별도 implementation child issue 발의

## Reversibility

spec 단계는 reversible. 구현 단계에서 DB schema 변경 발생 시 별도 보드 승인.

## 의존성

없음 — 즉시 시작.
