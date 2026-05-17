---
name: "Vendor trust signal 축 강화 (PACAA-743 G 결정 후속)"
assignee: "ceo"
---

# Vendor trust signal 축 강화 (PACAA-743 G 결정 후속)

## 배경
PACAA-743 에서 보드가 시나리오 G (리뷰 스크래핑/aggregation 폐기, trust signal 다른 축 강화) 선택. Legal 자문 (PACAA-764) 결과 무단 스크래핑/익명+요약 재게시는 금지 수준. 사용자 가치 ('이 vendor 신뢰할 만한가') 를 review 외 축으로 합법·저비용 달성하는 것이 목표.

## 목표
Vendor card / vendor 상세 페이지에서 buyer 가 vendor 신뢰도를 판단할 수 있는 trust signal 체계 정의 + 표시 spec 작성.

## 5축 후보 (CEO/Legal 분석 기반)
1. 사업자등록 (business registration) — 사업자등록증 확인 여부
2. 통신판매업 신고 (telesales registration) — 신고 번호 (B2C 모델일 때만 의미, 미신고 vendor 도 정상 적용)
3. KS 인증 / 산업 인증 (corrugated KS, 친환경 인증 등)
4. 납품 실적 (delivery track record) — 거래 기업, 누적 박스 수량 등
5. Founder attestation — Packlinx founder 검증 stamp (수동 sample 기반)

## 본 child 의 deliverable (CMO 책임)
- 위 5축 중 vendor 적합도/표시 우선순위 결정 (감산 + 우선순위 + UI label 한국어 카피)
- vendor 유형별 (박스/인쇄/기계/도매/3PL) 적용 가능 매트릭스
- vendor card / vendor detail 페이지에 표시할 UI mock 또는 카피 spec
- buyer 시점에서 noise/over-claim 방지 가드 (예: 사업자등록 = 기본, KS 인증은 별도 badge)
- buyer 가 신뢰도 위계를 한눈에 이해 가능한 표시 패턴

## 분리 권장 (CMO spec 완료 후 별도 child 발의)
- BE/CTO: vendor 데이터 schema 컬럼 추가 + admin/founder 입력 UX
- FE: vendor card / vendor detail 페이지 렌더링
- Content: vendor onboarding form 항목 추가

## 비-목표 (제외)
- 외부 리뷰 스크래핑 (PACAA-743 에서 폐기 결정)
- 자체 review/평점 UG
