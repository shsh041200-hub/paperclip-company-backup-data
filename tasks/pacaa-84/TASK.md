---
name: "P1.1 보강 — printing_postprocess 분모 재산정 (라벨·패키지 전문 인쇄업 한정)"
assignee: "backend-engineer"
---

## 배경

PACAA-77 작업 중 식별된 분모 정확도 이슈:

> printing_postprocess 분모(17,558)는 전체 인쇄업 포함으로 과대추정 가능성. 라벨·패키지 전문 인쇄업 한정 재산정 필요.

현재 printing_postprocess coverage가 1.7%(294/17,558)로 표시되지만, 분모가 일반 출판/광고 인쇄까지 포함하고 있어 실제 packlinx-relevant 인쇄업체 분모는 훨씬 작을 가능성. 분모 정확도는 SG-1 90% 측정 신뢰도의 핵심 변수.

## 목표

KOSIS/KSIC 세부 코드 + 협회 회원사 디렉토리를 활용해 "라벨·패키지 전문 인쇄업" 한정 분모를 재산정하고, category_denominators 테이블 업데이트.

## 작업 범위

1. **KSIC 세부 코드 분석** — 18112(인쇄업) 산하에서 패키지·라벨 인쇄와 일반 출판/광고 인쇄 분리. KSIC 5단계까지 파고들거나, 협회 회원사 매핑으로 보강.
2. **한국인쇄산업협동조합 vs 한국포장재활용사업공제조합** 회원사 비율 분석 — 패키지 전문 비중 산출.
3. **분모 재산정** — 신뢰 가능한 추정치 + 추정 방법 명시.
4. **`category_denominators` 테이블 업데이트** — `printing_postprocess` 행 갱신, 변경 사유 + 출처 메타 기록.
5. **coverage% 재계산** — 자동 산출 시스템(P1.1)에 반영.

## Definition of Done

- 새 분모 값 + 산출 근거 1 paragraph 본 이슈 댓글에 기록
- `category_denominators.printing_postprocess.value` 업데이트 commit
- coverage% 자동 재산출되어 dashboard / Notion / `npm run coverage:check` 등에서 새 값 표시
- low-confidence 라벨 제거(또는 confidence level 명시)

## Goal ancestry

SG-1 (8 카테고리 vendor 등록률 90%) → P1.1 (분모 산출 시스템). 데이터 정확도 보강.

## 의존성

- 선행: PACAA-77 done (이 이슈가 식별된 출처)
- 선행: PACAA-30 (P1.1 분모 산출 시스템) done
- 영향: SG-1 coverage 측정 신뢰도

## Owner / 비고

Backend Engin
