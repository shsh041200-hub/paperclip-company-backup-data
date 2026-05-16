---
name: "[후속 PACAA-737] FE V1 real-data wire-up (vendor_telesales_checks → vendorModel)"
assignee: "ceo"
---

**부모**: PACAA-737 (보드 옵션 B 결정). V1 mock vendorModel='A' → 실데이터 wire-up.

## 목적
PACAA-748 BE 파이프라인 (`vendor_telesales_checks` 2767건) 결과를 V1 페이지의 `vendorModel` 에 wire.

## 매핑
```ts
function resolveVendorModel(company): VendorModel {
  const check = company.telesales_check;  // join from vendor_telesales_checks
  if (!check) return 'unknown';
  if (check.result === 'found') return 'B';
  if (check.result === 'not_found') return 'A';
  if (check.result === 'exempt') return 'unknown';  // 배지/박스 hide
  return 'unknown';
}
```

## 작업 범위
- `app/internal/vendor-redesign/v1/[slug]/page.tsx` — vendorModel mock 제거 + join query 추가
- Supabase query: `companies` LEFT JOIN `vendor_telesales_checks ON vendor_id` (최신 row)
- BE 협조 필요 시: helper SQL view 또는 typed query

## ANTI 준수
- not_found vendor 를 위험/미신고/주의 카피 X (기존 ANTI 그대로)
- 동명이인 위험 (BE 명시) → UI 에 "분류 정정 요청" 링크 노출 (PACAA-XXX SLA implementation 과 연동)

## Acceptance
1. Production main 머지 + Vercel READY
2. 3 케이스 라이브 검증:
   - found vendor → Model B (배지 "샘플·소량부터 가능", CTA "샘플 신청"+"견적 문의")
   - not_found vendor → Model A (배지 "기업 거래 전문", §20 disclaimer, CTA "견적 문의")
   - exempt or NULL vendor → unknown (배지/박스 hide, CTA "견적 문의" 단일)
3. ANTI grep 0 (위험/미신고
