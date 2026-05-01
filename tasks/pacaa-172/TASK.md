---
name: "[CTO 배포] corrugated-box-supplier-selection FAQPage schema + hreflang + 내부 링크"
assignee: "cto"
---

## 배경

[PACAA-170](/PACAA/issues/PACAA-170) CMO 분석 완료. corrugated-box-supplier-selection 가이드에 FAQPage schema, hreflang ko-KR, /products/box 내부 링크 3가지 누락 확인.

## 배포 요청 사항

### 1. FAQPage JSON-LD schema

`<head>` 또는 article 하단에 아래 JSON-LD를 삽입:

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "골판지 박스 업체 선택 시 견적 단가 외에 꼭 확인해야 할 항목은 무엇인가요?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "MOQ(최소주문수량), 납기(리드타임), 인쇄 역량(플렉소/옵셋), 물류 접근성, 인증(FSC·ISO 등), 샘플 대응 총 6가지입니다. 박스 단가가 개당 50원 낮아도 납기 지연 하루면 그 이상의 기회비용이 발생합니다."
      }
    },
    {
      "@type": "Question",
      "name": "골판지 박스 납기(리드타임)는 보통 얼마나 걸리나요?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "표준 무인쇄·1도 인쇄 박스는 5~7영업일, 다색 인쇄나 특수 합지 구조는 10~15영업일이 일반적입니다. 설·추석·연말 성수기에는 2~3일이 추가되며, 납기 기산점이 발주 확정일인지 입금 확인일인지 반드시 확인해야 합니다."
      }
    },
    {
      "@type": "Question",
      "name": "플렉소 인쇄와 옵셋 합지의 차이는 무엇인가요?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "플렉소 인쇄는 골판지 원단에 직접 인쇄하는 방식으로 1~3도 단색에 적합하고 단가가 낮습니다. 옵셋 합지는 별도 인쇄지를 골판지에 부착하는 방식으로 풀컬러·고해상도 표현이 가능하지만 단가가 높고 납기가 깁니다."
      }
