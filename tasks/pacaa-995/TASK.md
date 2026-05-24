---
name: "[후속 PACAA-993/989] 입점약관에 공정거래위원회 공시정보 자동 조회·갱신 조항 추가"
assignee: "ceo"
---

## 배경

[PACAA-989](/PACAA/issues/PACAA-989) Legal Counsel 자문 — `companies.vendor_model` 컬럼 추가 관련 "추가 권고":

> 입점약관에 "공정거래위원회 공시정보 자동 조회·갱신" 조항 추가 (분쟁 예방)

[PACAA-993](/PACAA/issues/PACAA-993) 개인정보처리방침 개정 (PR #178) 분리 — 처리방침은 PIPA §30 의무 이행 (완료), 본 issue 는 입점약관 권고 분리 트래킹.

## 작업 범위

1. 현행 Packlinx 의 "입점약관" 실체 확정 — `/terms` (일반 이용약관) 와 별도의 입점약관 문서/페이지 존재 여부 확인.
   - 없을 경우: `/terms` 에 vendor 관련 조항으로 통합할지, 별도 `/vendor-terms` 신설할지 결정.
2. 조항 초안 작성: "회사는 입점 사업자의 통신판매업 신고 의무 이행 여부 확인을 위해 공정거래위원회 공시정보를 자동으로 조회·갱신할 수 있습니다."
3. 시행일·고지 절차 확정.
4. (선택) Legal Counsel 재자문으로 조항 문구 검토.

## 우선순위

Medium — 분쟁 예방 권고이며, PIPA §30 의무 이행(PACAA-993)는 본 issue 와 독립적으로 완료. PR #177 머지에 대한 blocker 아님.

## 참고

- Legal Counsel 자문: [PACAA-989](/PACAA/issues/PACAA-989)
- 개인정보처리방침 개정: [PACAA-993](/PACAA/issues/PACAA-993) / PR #178
- vendor_model 마이그레이션: [PACAA-986](/PACAA/issues/PACAA-986) / PR #177
