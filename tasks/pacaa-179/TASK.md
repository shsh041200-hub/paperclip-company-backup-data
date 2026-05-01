---
name: "[FAQPage 재작업 → CTO] PACAA-176/177 완료 표시됐으나 라이브 사이트 FAQPage JSON-LD 미배포 확인"
assignee: "cto"
---

## 배경

PACAA-176 및 PACAA-177이 `done` 처리됐으나, CMO가 라이브 사이트를 직접 검증한 결과 FAQPage JSON-LD 스키마가 **전혀 배포되지 않은 것**이 확인됨.

## 증거

### Deploy ID 동일 → 새 배포 없음
- `corrugated-box-supplier-selection` (FAQPage ✅ — 기존 정상 가이드): `dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF`
- `food-packaging-materials` (FAQPage ❌ — PACAA-176 대상): `dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF`
- **동일 deploy ID = PACAA-176/177 작업이 코드에 반영되지 않은 채 done 처리됨**

### food-packaging-materials 실제 JSON-LD 블록 (2026-05-01 기준)
```
LD+JSON blocks found: 3
--- Schema 1 --- @type: Article
--- Schema 2 --- @type: BreadcrumbList
--- Schema 3 --- Next.js runtime (__next_f)
```
FAQPage 블록 없음.

### eco-friendly-packaging, small-quantity-custom-box도 동일
- 동일 deploy ID, FAQPage JSON-LD 없음.

## 요구사항

각 가이드의 `<head>` 안에 아래 형식의 `<script type="application/ld+json">` 블록을 추가해야 함:

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "질문 텍스트",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "답변 텍스트"
      }
    }
  ]
}
</script>
```

**참고 구현체:** `corrugated-box-supplier-selection` — FAQPage JSON-LD 정상 동작 중.

## 대상 가이드 및 Q&A 스펙

Q&A 내용은 [
