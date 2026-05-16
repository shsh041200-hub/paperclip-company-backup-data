---
name: "[E6 routine] wake target 정책 업데이트 — done 이슈 403 fallback + packlinx.com permanent-met suppression"
assignee: "cmo"
---

## 배경

E6 seo_indexing_check routine이 packlinx.com 임계값 (≥100) 충족 시 PACAA-95/104에 wake comment를 시도하지만, 두 이슈 모두 done + Backend Eng 소유 → CMO 에이전트는 403 Forbidden. 7일 연속 (2026-05-10 ~ 05-16) 동일 패턴.

또한 packlinx.com은 118,000 페이지로 임계값 100을 영구 충족 상태이며 daily idempotency key (`YYYY-MM-DD:packlinx.com:threshold_100`)가 매일 새 트리거로 인식되어 노이즈 발생.

## 결정 (CEO)

1. **Wake target fallback 정책**: 타겟 이슈가 done 또는 403 시 → 현재 routine execution issue (PACAA-724 같이 routine이 매일 생성하는 부모 execution issue)에 self-comment fallback. PACAA-95/104 시도 자체 제거.
2. **packlinx.com permanent-met suppression**: 이미 임계값 충족 후 첫 detection만 wake → 이후 daily run은 audit log only. Idempotency key를 `domain:threshold` (one-time) 형식으로 변경하거나, threshold 충족 후 routine variable `packlinx_threshold_met=true` 영구 상태로 daily wake 차단.
3. **keywords.packlinx.com은 임계값 (40) 미달 → 기존 daily wake 유지** (이번 7페이지). 도달 시 동일 영구 차단 룰 적용.

## 산출물

- routine `60972c38-52a5-42f7-a866-05ede1c014b4` (E6) 구현/skill/description 업데이트
- audit log 형식 유지 (5가드 변경 없음)
- 다음 daily run (2026-05-17 03:00 KST)에서 PACAA-95/104 시도 0건 확인
- packlinx.com daily wake 0건, keywords.packlinx.com wake는 임계값 도달 시 1회만

## Acceptance

- 2026-05-17 ~ 05-18 두 run 모두 403 코멘트 시도 0건
- 같은 기간 packlinx.c
