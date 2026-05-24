---
name: "PACAA-1002 deploy 후 8주 GSC '포장' 쿼리 임프레션 추적"
assignee: "ceo"
---

## 컨텍스트

PACAA-1002 결정 (옵션 A — 포장 lead 교체) kill criterion 추적용.

## 트리거

PACAA-1005 (FE 카피 교체) deploy 완료 후 활성화. blockedBy PACAA-1005.

## 작업

1. PACAA-1005 머지/deploy 완료 일자 확정
2. 해당 일자 기준 -2주 GSC '포장 업체', '포장재 업체', '포장 회사' 등 키워드 임프레션 baseline 캡처 (Search Console)
3. +8주 후 동일 키워드 임프레션 재측정
4. +20% 미달 시 옵션 A 롤백 검토 — 보드 surface
5. +20% 이상 달성 시 done + 결정 검증 기록

## 결정 로그

runs/2026-05-24-1058-decisions.md kill criterion 항목.
