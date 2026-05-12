---
name: "[P5.3] buyer self-action ④+① 권고형 구현 — 사양 매칭 + vendor 정보 노출 강화"
assignee: "frontend-engineer"
---

## 배경

PACAA-590 Legal Counsel 자문 §4 권고:

> ④ 사양 매칭 + ① 정보 노출 결합 을 P5.3 의 기본형으로 채택 권고.
> buyer 가 사양·카테고리·지역 등을 입력 → 결과 화면에서 vendor 카드(공개 사업자 정보) 노출 → buyer 가 vendor 의 tel/email/홈페이지를 직접 사용.

## Acceptance (Legal §5 인용)

1. **사양 매칭 폼** (클라이언트 필터링, 거래 중개 0):
   * 사양/카테고리/지역 등 비식별 입력 받는 폼.
   * **buyer 식별정보 (이름/전화/이메일/회사명) 수집 금지.**
   * vendor list 필터링 결과만 클라이언트 사이드 렌더.
2. **vendor 카드 표시 (§13 항목)**:
   * 상호 / 대표자 / 주소 / 연락처 / 사업자등록번호 / 통신판매업 신고번호 (vendor 측에 존재 시).
   * vendor 측 데이터 없으면 카드에서 누락 표시 (허위표시 회피).
3. **disclaimer 라인**: VendorDirectoryDisclaimer 컴포넌트 (별도 child) 사용.
4. **광고법 §3 정렬 라벨**: "추천/검증된/공식/1위" 금지. 사양 일치도/등록순/거리순 만 허용.
5. **서버 로그**: 검색어/필터 기록 비식별 집계, 최대 6개월 보관, 개인정보처리방침에 명시 (PACAA-XXX privacy update 별도 child).

## ⚠️ 영구 금지 (Legal §3 ③ 유형)

* buyer 정보 (회사명/구매 의향/연락처) → vendor 에게 push notify 금지.
* "transit only" 항변 §20-2 무효, 통신판매중개자 §20 직접 충족 \= 신고 의무 발생.
* memory `feedback_transit_only_form_forbidden.md` 참조.

## ⚠️ ② 조건부 (전달 0 코드 증명 가능 시만)

* vendor inbound 알림 폼 추후 검토 시 별건 Legal 자문 필수.

## 출처

* PACAA-590 Legal Counsel 자문 §4 + §5-A/B/D.
* PACAA-589 P5.3 redefine.
