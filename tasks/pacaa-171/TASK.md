---
name: "[corrugated-box guide → CTO] FAQPage schema + hreflang + 내부링크 패치 배포 요청"
assignee: "backend-engineer"
---

## 요청 배경

CMO 감사 결과 `/guides/corrugated-box-supplier-selection` 페이지가 기술 SEO 3개 항목에서 미흡함을 확인.

## 현재 상태

| 항목 | 상태 |
|------|------|
| FAQPage JSON-LD 스키마 | ❌ 없음 |
| hreflang ko-KR | ❌ 없음 |
| 내부 /products/box 링크 | ❌ 없음 (plain text만 존재) |

## 요청 사항 (3가지)

### 1. FAQPage JSON-LD 삽입

`/guides/corrugated-box-supplier-selection` 페이지 `<head>` 또는 콘텐츠 데이터에 아래 JSON-LD 추가:

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "골판지 박스 최소주문수량(MOQ)은 얼마인가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "대형 제조사는 1,000~3,000박스, 중소 제조사는 300~1,000박스가 일반적입니다. 업체별 MOQ가 상이하므로 자사 월간 소요량과 창고 보관 여력을 먼저 파악한 뒤 업체를 선별하시기 바랍니다." }
    },
    {
      "@type": "Question",
      "name": "골판지 박스 납기는 얼마나 걸리나요?",
      "acceptedAnswer": { "@type": "Answer", "text": "표준 박스(무인쇄 또는 1도 인쇄)는 보통 5~7영업일, 다색 인쇄나 특수 합지 구조는 10~15영업일이 일반적입니다. 성수기(설·추석·연말)에는 2~3일 추가됩니다." }
    },
    {
      "@type": "Question",
      "name": "골판지 박스 업체 샘플 비용은 얼마인가요?",
      "acceptedAnswer": { "@type": "Answer", "text": "업체마다 상이합니다. 무료 샘플을 제공하는 곳도 있으나, 맞춤 규격의 경우 금형비(목형비)가 별도 청구되는 경우가 많습니다(보통 15~30만 원). 견적 요청 시 샘플 비용 여부를 함께 확인하시기 바랍니다." }
    },
    {
