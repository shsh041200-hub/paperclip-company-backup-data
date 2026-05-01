---
name: "[FAQPage → CTO] 이사박스-대량구매-가이드 + 이사박스-사이즈-규격 FAQPage JSON-LD 추가"
assignee: "cto"
---

## 배경

[PACAA-170](/PACAA/issues/PACAA-170) P5.4 감사에 포함된 이사박스 가이드 2개에 FAQPage JSON-LD가 없습니다. 추가 요청합니다.

## 대상 가이드 및 FAQPage JSON-LD 스펙

### 1. `/guides/이사박스-대량구매-가이드`

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "이사박스 대량 구매 시 골판지와 단프라 중 무엇을 선택해야 하나요?",
      "acceptedAnswer": { "@type": "Answer", "text": "1회성 이사에는 골판지(800~2,500원/개)가 적합하고, 반복 물류·창고 운영에는 단프라(3,000~8,000원/개)가 장기적으로 유리합니다. 단프라는 50~200회 이상 재사용 가능해 월 500개 이상 사용 시 총 비용이 절감됩니다." }
    },
    {
      "@type": "Question",
      "name": "이사박스 제조사 직거래 vs 도매상, 어떤 채널이 유리한가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "월 500개 이상 구매 시 제조사 직거래로 10~30% 절감이 가능합니다. 소량 구매나 다양한 사이즈 혼합 발주라면 재고를 보유한 도매상이 납기와 유연성 면에서 유리합니다." }
    },
    {
      "@type": "Question",
      "name": "이사박스 대량 발주 시 납기는 얼마나 걸리나요?",
      "acceptedAnswer": { "@type": "Answer", "text": "일반 재고 물량은 1~3 영업일, 별도 제작(커스텀 사이즈·인쇄 포함)은 5~10 영업일이 일반적입니다. 이사 성수기(3~5월, 9~11월)에는 납기가 2주 이상 지연될 수 있으므로 최소 2주 전 선발주를 권장합니다." }
    },
    {
      "@type": "Question",
      "name": "이사박스 골판지 등급(BF·CF·SSF)별 차이는 무엇인가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "BF(Basic Flu
