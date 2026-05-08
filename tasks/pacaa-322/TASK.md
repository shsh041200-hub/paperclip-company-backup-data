---
name: "비교→견적 의뢰 폼 plan (P0-4 plan-first)"
assignee: "cto"
---

## 목적

비교 결과 페이지에서 buyer 가 3개 vendor 에 한 번에 견적 요청 → Packlinx 가 lead 데이터 보유. **Vision 3축 동시 진전 (벤더 자가 참여 / default surface / 모방 난이도) 후보 1개**. Houzz Pro 검증 패턴.

**plan-first ticket.** implementation 은 별도 child (이 ticket 의 sub-ticket) 로 fork. 보드 acceptance 게이트 plan 단계.

## Scope (CTO plan 작성, M effort 추정 — 데이터 모델 + Legal + Backend + Frontend 교차)

### Plan 작성 항목

1. **데이터 모델:** lead capture table (buyer email/회사/수량/마감/요구사항 + 선택된 vendor IDs + status). 신규 schema 작성.
2. **PIPA 준수 (Legal Counsel 필수 자문):** 개인정보 수집 동의 문구 + 보관 기간 + 처리 방침 update + 통신판매업 신고 영향 점검. `legal-consult` skill 호출.
3. **vendor 측 분배 채널:** 받은 lead 를 vendor 에게 어떻게 전달? 이메일 / vendor portal / dashboard. PoC = 이메일 자동 발송.
4. **frontend UI:** `/compare` 하단 단일 폼 + 입력 검증 + 성공 화면.
5. **backend API:** POST /api/leads (rate limit, spam 방어, 이메일 발송 큐).
6. **측정:** 폼 진입율 / 완료율 / vendor 응답 시간.

### Plan deliverable

- `$AGENT_HOME/plans/pacaa-308-p0-4-quote-form.md` 형식 plan document.
- plan revision 후 CEO 에 `request_confirmation` 으로 surface, CEO 가 보드 escalate.

### Out of scope (이 ticket 에서)

- 실제 코드 작성. plan 승인 전 코드 0줄.
- vendor portal 신규 surface (PoC = 이메일).

## Acceptance (plan ticket 한정)

- [ ] plan document 7개 섹션 (모델/PIPA/분배/UI/API/측
