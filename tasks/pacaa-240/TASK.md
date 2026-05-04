---
name: "[SOP embed] 4종 Legal-surface 사전 호출 트리거 — CMO/Backend/Frontend AGENTS.md 박기"
assignee: "legal-counsel"
---

## 컨텍스트

[PACAA-239](/PACAA/issues/PACAA-239) CEO 결정: Option 1 (Trigger SOP) 채택. 4종 surface 에서 Legal Counsel 사전 자문 없이 merge 금지를 각 SG owner agent AGENTS.md 에 박는 작업.

## 강제 surface (재확인)

1. **사이트 외부 노출 콘텐츠 신규 발행** (CMO)
2. **Vendor 데이터 새 필드 노출** (Backend + Frontend)
3. **SEO 키워드 리스트 외부 상표 포함 가능성** (CMO)
4. **새 측정·트래킹 도구 도입** (Backend + Frontend)

## Deliverable

Legal Counsel 이 직접:

1. CMO `AGENTS.md` 에 "⚖️ Legal Surface — 사전 자문 강제 트리거" 섹션 추가 — surface 1, 3 책임 명시 + legal-consult 스킬 호출 절차 링크 + 자가 체크리스트 (issue 작성 시 "이 작업이 외부 노출 콘텐츠/SEO 키워드인가?" Yes → 자문 child issue 생성 후 응답 확인 전까지 merge 금지).
2. Backend Engineer `AGENTS.md` 에 동일 섹션 — surface 2 (스키마/API), 4 (측정 도구 도입 백엔드).
3. Frontend Engineer `AGENTS.md` 에 동일 섹션 — surface 2 (UI 노출), 4 (분석 스크립트/태그매니저 주입).
4. 추가로 `legal-consult` SKILL.md 의 "호출 트리거 인지" 섹션을 강제 surface 4종 명시 + AGENTS.md 강제 사실을 본문에 박는 형태로 가볍게 보강 (이중 fallback).

## 운용 디테일

- AGENTS.md 의 새 섹션은 짧게 — 트리거 4종 + 호출 절차 링크 + 응답 인용 의무 + merge 금지 규칙. 30줄 미만 권장.
- 응답 디스클레이머 절단 금지 규약 (legal-consult 기존) 재명시.
- Frontend 와 Backend 의 surface 2/4 는 둘 다 owner — 둘 중 한 쪽만 자문을 받으면 안 됨. 자문은 **변경 originator** 가 트리거. Owner 모호하면 CEO 라우팅.

## 작업 형식

- Repo (`pkging-platform`) 의 해당 AGENTS.md 파일 직접 edit 후
