---
name: "[후속 PACAA-737] FE V1 UI 구현 — VendorModelBadge + VendorTradingBox + Legal disclaimer baking"
assignee: "ceo"
---

**부모**: PACAA-737 (보드 accept b38c793c). 최종 안 §A 라벨/카피 + §C 컴포넌트 + §D Legal 4건 baking.

## 컴포넌트 분리 (FE PACAA-745 권고)
- `app/internal/vendor-redesign/v1/[slug]/VendorModelBadge.tsx` — 서버 컴포넌트, 순수 표현
- `app/internal/vendor-redesign/v1/[slug]/VendorTradingBox.tsx` — 서버 컴포넌트
- `page.tsx` — vendorModel 계산 + 컴포넌트 조합

## prop 설계
```ts
type VendorModel = 'A' | 'B' | 'unknown'
// 1차 신호: vendor_telesales_checks.result (BE 파이프라인 결과)
//   found → 'B', not_found → 'A', exempt → 'unknown'
// 2차 신호 (옵트인 컬럼): 보드 재결재 후 추가, 1차 결과 override
```

## 카피 baked (CMO PACAA-744 권고)
- A 배지: `기업 거래 전문` (네이비 또는 딥그린 강조색)
- B 배지: `샘플·소량부터 가능`
- A 박스: "초대량 B2B 전문 공급사. 견적은 전화·이메일로 진행됩니다."
- B 박스: "샘플부터 소·대량 거래 가능. 웹 카탈로그에서 직접 확인하고 견적 요청하세요."
- A CTA: `견적 문의` 단일 (sticky)
- B CTA: `샘플 신청` (1st primary) + `견적 문의` (2nd)
- unknown: 배지/박스 hide + CTA `견적 문의` 단일

## Legal 필수 4건 baked (PACAA-747)
1. Model A `VendorTradingBox` 내 §20 disclaimer (정확 카피):
   > "본 업체는 통신판매업 신고 사업자가 아닙니다. 거래·계약·결제·환불 등 모든 절차는 구매자와 업체가 직접 진행하며, Packlinx는 거래 당사자가 아닙니다."
2. 배지 옆 (i) 아이콘 hover/주석:
   > "통신판매업 신고 정보 + vendor 자가신고 기반 거래 형태 분류 — 품질·신뢰도 평가 아님"
3. 페이지 하단 분류 출처 표기:
   > "분류 근거: 공정위 통신판매사업자 공시 + vendor 자가신고"
4. Model B footer 기존 §20① 통신판매중개
