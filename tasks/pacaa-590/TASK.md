---
name: "[Legal 자문] P5.3 redefine — buyer self-action legal-cleared form 범위 정의"
assignee: "legal-counsel"
---

## 배경

PACAA-589 (Goals 재검토) 보드 결정 q4\_b 로 P5.3 (기존 "견적 문의 폼") 을 redefine: 통신판매업 + 표시광고법 + PIPA 모두 cleared 인 buyer self-action form 정의. 견적 의뢰 자체는 PACAA-466 으로 폐지 확정.

## 자문 요청

현재 Packlinx 는 통신판매업 미신고 + 거래 중개 회피 모드 운영. buyer 가 vendor 와 직접 연결되도록 유도하는 form 중 어떤 유형이 안전한지 정의 필요:

1. **단순 vendor 정보 노출** (전화/이메일/링크) — 현재 운영. Safe?
2. **vendor 측 inbound 알림 폼** (buyer 가 vendor 에게 직접 연락 의사 전달, Packlinx 는 메시지 중개 안 함, 단순 노출 안내) — 가능?
3. **buyer 자기 정보 입력** (회사명/구매 의향) → vendor 에게 push notify, Packlinx 는 transit only. 통신판매업 trigger 여부?
4. **카테고리/사양 매칭 폼** (buyer 가 사양 입력 → vendor list 필터링, 거래 중개 0) — Safe?

각 유형에 대해:

* 통신판매업 신고 의무 발생 여부
* 표시광고법 risk (광고 표현 한계)
* PIPA (buyer 정보 수집·이용 동의 요건)
* 권고/대안

## Acceptance

* 4 유형별 cleared/blocked/조건부 판정.
* 권고 유형 1개 + 구현 가이드 (필수 disclaimer, 동의문, 데이터 보존 기간).

## 후속

자문 done 후 CEO 가 FE child issue 발의 → P5.3 구현.
