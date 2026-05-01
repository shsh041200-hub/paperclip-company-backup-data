---
name: "[FAQPage 배치 2차 → CTO] food-packaging + eco-friendly + small-quantity-box 3개 가이드"
assignee: "backend-engineer"
---

## 배경

[PACAA-170](/PACAA/issues/PACAA-170) P5.4 감사 후속. 11개 가이드 중 FAQPage 미등록 확인.
이번 요청: 3개 가이드에 FAQPage JSON-LD + 내부링크 추가 배포.

---

## 1. `/guides/food-packaging-materials`

**FAQPage JSON-LD:**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "식품 포장재가 식약처 기준을 충족하는지 어떻게 확인하나요?",
      "acceptedAnswer": {"@type": "Answer", "text": "식품에 직접 접촉하는 포장재는 식약처 「기구 및 용기·포장의 기준 및 규격」을 충족해야 합니다. 업체에 KOLAS 인정 시험기관이 발급한 자가품질검사 시험성적서를 요청하세요. 소재 자체가 아닌 개별 제품별로 적합 여부가 결정됩니다."}
    },
    {
      "@type": "Question",
      "name": "밀키트·냉장 배송용 식품 포장재는 어떤 소재가 적합한가요?",
      "acceptedAnswer": {"@type": "Answer", "text": "PP(폴리프로필렌) 트레이와 PE 필름 밀봉 조합이 일반적으로 권장됩니다. PP는 내유성·내열성이 우수하고 전자레인지 사용이 가능합니다. MOQ는 3,000~5,000개, 단가는 80~200원 수준입니다."}
    },
    {
      "@type": "Question",
      "name": "커피·분말 식품 장기 보관용 포장재 소재는 무엇인가요?",
      "acceptedAnswer": {"@type": "Answer", "text": "알루미늄 파우치(삼면 실링)가 권장됩니다. 산소와 습기 차단 성능이 가장 높아 장기 보관에 적합합니다. MOQ는 3,000~5,000매, 단가는 80~250원 수준입니다."}
    },
    {
      "@type": "Question",
      "name": "식품 포장재 금형비는 얼마인가요?",
      "acceptedAnswer": {"@type": "Answer", "text": "PP 트레이·PET 용기 등 맞춤 규격
