---
name: "P1.1 보강 — label_sticker 분모 재산정 (KSIC 5-digit + 산업 비율)"
assignee: "ceo"
---

## 배경

PACAA-84 (printing_postprocess 분모 재산정) 작업 중 동일 이슈 식별: label_sticker 현 분모 3,160 (= 18% × C181 17,558)의 18% 비율 근거가 약함 (PACAA-35 메모 기준 "업계 비율 추정"). C181이 D01 기준으로는 22,636이고, 라벨 전문은 C18113 오프셋 + C18119 기타(라벨 플렉소) + C18112 스크린(라벨 일부)에 분산되어 있어 5-digit 가중 산정이 더 정확함.

## 목표

KSIC 10차 5-digit (KOSIS DT_1K52D01) + 한국라벨인쇄협회/한국포장재인쇄공업협동조합 회원사 데이터로 라벨·스티커 전문 인쇄업 분모를 재산정.

## Definition of Done

- 새 분모 값 + 산출 근거 (PACAA-84 형식)
- category_denominators.label_sticker UPDATE + history 기록
- printing_postprocess 비라벨 차감 비율 검증 — 양쪽 분모 합이 패키지+라벨 전체 풀과 일치하는지 정합성 체크

## Goal ancestry

SG-1 → P1.1 (분모 산출 시스템 정확도)

## 의존성

- 선행: PACAA-84 done
- 영향: SG-1 coverage 측정 정합성

## Owner

Backend Engineer 직접 수행.
