---
name: "[FAQPage 배치 3차 → CTO] corrugated-flute-types + cosmetic + electronics + packaging-material + tape + shipping-box 6개 가이드"
assignee: "cto"
---

## 배경

[PACAA-170](/PACAA/issues/PACAA-170) P5.4 감사 결과 — P5.4 후보 9개 중 6개 가이드에 FAQPage JSON-LD가 아직 없습니다. 아래 6개 가이드에 FAQPage schema 삽입 및 배포를 요청합니다.

---

## 대상 가이드 및 FAQPage JSON-LD

### 1. `/guides/corrugated-flute-types`

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "골판지 A골과 B골의 실질적인 차이는 무엇인가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "A골은 두께 약 5mm에 완충성이 최고 수준이며 가전·가구 등 무거운 제품과 장거리 운송에 적합합니다. B골은 두께 약 3mm로 가장 범용적인 택배 박스 표준이며 완충성과 인쇄 적합성의 균형이 좋습니다. B골 대비 A골 단가는 약 15~20% 높습니다." }
    },
    {
      "@type": "Question",
      "name": "제품 무게가 5kg을 넘으면 어떤 골을 선택해야 하나요?",
      "acceptedAnswer": { "@type": "Answer", "text": "3~5kg 제품은 B골로 충분하지만 5kg 초과 시에는 A골 사용이 권장됩니다. 10kg 이상 제품에는 A골, 20kg 초과 중량물이나 5단 이상 적재가 필요한 경우에는 AB골(이중골)을 선택해야 합니다." }
    },
    {
      "@type": "Question",
      "name": "E골 박스는 화장품 포장에 충분한 강도인가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "500g 이하 화장품·소형 전자기기처럼 파손 민감도가 낮은 제품에는 E골이 적합합니다. E골은 두께 약 1.5mm로 인쇄 품질이 최상급이며, B골 대비 개당 단가가 20~25% 낮아 배송비와 포장 원가를 동시에 절감할 수 있습니다." }
    },
    {
      "@type": "Question",
      "name": "AB골(이중골)은 언제 반드시 선택해야 하나요?",
