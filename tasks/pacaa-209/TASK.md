---
name: "[P5.4 Phase H → CTO] /guides/packaging-machinery-guide 발행 (포장기계·자동화)"
assignee: "cto"
---

## 목적
P5.4 8번째(마지막) 카테고리 가이드: 포장기계·자동화 (packaging machinery & automation)

## 구현 요구사항
- **Route**: `/guides/packaging-machinery-guide`
- **목표 분량**: ≥1500자 (한국어 본문)
- **대상 독자**: 포장 자동화 도입을 검토하는 B2B 구매 담당자

## 필수 섹션 (8개)
1. 포장기계 종류 개요 (충전기·밀봉기·라벨러·박스포장기·팔레타이저)
2. 자동화 도입 ROI — 인건비 절감 계산식, 손익분기점
3. 국내 주요 제조사 비교 (3~5개사)
4. MOQ·납기·설치 조건
5. 유지보수·소모품·AS 네트워크
6. 식약처·KC 인증 요건 (식품·의약품 라인)
7. 도입 체크리스트 (발주 전 확인 사항)
8. 구매 프로세스 요약

## FAQPage JSON-LD (필수 — 페이지 <head>에 삽입)
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {"@type":"Question","name":"포장기계 도입 시 최소 발주 수량은?","acceptedAnswer":{"@type":"Answer","text":"기종에 따라 다르지만 국내 제조사 기준 1대부터 발주 가능합니다. 단 맞춤 제작형은 3개월 이상 납기가 필요합니다."}},
    {"@type":"Question","name":"자동화 포장기계 ROI는 얼마나 걸리나요?","acceptedAnswer":{"@type":"Answer","text":"생산량과 인건비에 따라 다르지만 월 생산량 10만 개 이상 라인에서는 평균 18~24개월 내 손익분기점에 도달하는 사례가 많습니다."}},
    {"@type":"Question","name":"식품 포장라인에 필요한 인증은?","acceptedAnswer":{"@type":"Answer","text":"식약처 식품 접촉 소재 기준 및 HACCP 적합 여부를 확인해야 합니다. 수출용 라인은 CE 마킹도 요구됩니다."}},
    {"@type":"Question","name":"포장기계 AS 네트워크는 어떻게 확인하나요?","acceptedAnswer":{"@type":"Answer","text":"계약 전 제조사의 전국 AS 거점 수와 평균 출동 시간을 확인하세요. 수도권 외 지
