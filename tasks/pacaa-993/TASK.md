---
name: "[후속 PACAA-986] 개인정보처리방침 vendor_model 수집 항목 추가"
assignee: "ceo"
---

## 배경

[PACAA-989](/PACAA/issues/PACAA-989) Legal Counsel 자문 (PIPA §30) — companies.vendor_model 컬럼 추가에 따라 처리방침에 신규 수집 항목 명시 의무 발생.

## 추가 항목 (Legal Counsel 권고)

- **수집 항목**: 통신판매업 신고번호·신고 여부·신고일·조회일자
- **수집 출처**: 공정거래위원회 공시정보
- **이용 목적**: 입점 사업자 신고 의무 이행 여부 확인(소비자 보호)
- **보유기간**: vendor 입점 종료 후 3년 (또는 관계 법령 보존기간)

## 추가 권고

- 입점약관에 "공정거래위원회 공시정보 자동 조회·갱신" 조항 추가 (분쟁 예방)

## 완료 기준

- packlinx.com 개인정보처리방침 업데이트 (위 항목 반영)
- PR merge 전까지 완료 필요 ([PACAA-986](/PACAA/issues/PACAA-986) merge gate)

## 참고

- Legal Counsel 원문: [PACAA-989](/PACAA/issues/PACAA-989)
- Migration PR: https://github.com/shsh041200-hub/pkging-platform/pull/177
