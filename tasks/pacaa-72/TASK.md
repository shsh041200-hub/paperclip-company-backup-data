---
name: "buyer 경험 품질 검토 + 페어 2 Designer 검토 (PACAA-71 트리거 발화)"
assignee: "ceo"
---

## 발화 경위

PACAA-71 보류 항목 트리거를 보드가 수동 발화 (2026-04-29). 원래 STATE 트리거(P1.3 완전 종료)보다 앞당김. → STATE 미충족 발화이므로 P1.3 진행 보호 + 본 검토는 사이드로 진행.

## 검토 대상

1. **Goal 트리 buyer 경험 축 보강 필요성.**
   - 현재 Goal: SG-1(vendor) / SG-2(SEO) / SG-3(측정) / SG-4(vendor self-action) — 모두 **공급/측정** 축.
   - 약한 축: buyer가 머무는 이유(디자인/UX/신뢰), 콘텐츠 마케팅, 브랜드, buyer self-action 입구.
   - 핵심 위험: WUV 5,000 도달해도 buyer 5초 이탈 시 비전 실현 불가.
2. **페어 2 (다음 hire 라운드)에 Designer 추가 필요성.**
   - 현재 페어 1 = Backend Eng + CTO. 페어 2 구성 미결.
   - Designer 추가 vs 다른 역할(Frontend Eng, Content Marketer, Buyer Researcher 등) 비교.

## 산출물 (Acceptance Criteria)

- `plans/buyer_experience_review_v1.md` 작성: 4축(공급/수요/측정/거래) 커버리지 자가진단 표 + 신규 SG/P 후보 + 페어 2 후보 비교 + CEO 권고 한 줄.
- 보드 `request_confirmation` (idempotencyKey: `confirmation:{thisIssueId}:plan:v1`) — 옵션: 채택 / 수정 후 채택 / 보류 / 폐기.
- 보드 사인오프 시 → Goal 추가는 PACAA-25 트리 패치 issue로 분기, 페어 2 hire는 별도 hire issue로 분기. 본 issue는 'plan 사인오프' 단계까지.

## 우선순위 / 영향

- 사이드 priority. P1.3 (Backend Eng 진행) 어떤 경우에도 영향 금지 — 본 검토는 CEO 사이드 슬롯에서만 진행.
- 보드 결정 후 Goal 추가가 채택되어도 P1.3 완전 종료 전에는 신규 작업 시작 X.

## 출처

- 보류 항목 등록: PACAA-71 (deferred_items.md → archive로 이동, outcome: re-adopted, board manual trigger 2026-04-29).
- 트리거 발
