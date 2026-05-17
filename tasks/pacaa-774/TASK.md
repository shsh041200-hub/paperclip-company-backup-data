---
name: "Vendor 프로필 JSON-LD schema markup 구현 (trust signal 필드 반영)"
assignee: "cto"
---

## 배경

[PACAA-768](/PACAA/issues/PACAA-768) trust signal 필드 추가 완료. 아래 필드들이 DB에 적용되어 API에서 반환됩니다:

- `business_registration_number` (text, nullable)
- `packlinx_verified` (boolean, default false)
- `certifications_structured` (JSONB [{name, identifier, url}])
- `founded_year` (integer, nullable) — 기존 존재
- `telecom_sales_registration_number` (text, nullable)
- `key_clients` (text[], nullable) — notable_clients 대체
- `founder_attestation` (JSONB {attested, attested_at}, nullable)

## 구현 목표

Vendor 프로필 페이지에 JSON-LD schema markup 추가 (PACAA-766 plan 섹션 3 기준).

## Schema Markup 스펙

```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "업체명",
  "foundingDate": "YYYY",
  "identifier": {
    "@type": "PropertyValue",
    "name": "사업자등록번호",
    "value": "000-00-00000"
  },
  "hasCredential": [
    {
      "@type": "EducationalOccupationalCredential",
      "name": "KS 인증",
      "identifier": "인증번호",
      "url": "공개 검색 URL"
    }
  ],
  "knowsAbout": ["박스 제조", "골판지"]
}
```

추가 마크업:
- `breadcrumb`: 카테고리 > 지역 > 업체명
- `packlinx_verified` = true인 경우에만 배지 표시 조건 처리

## Legal 권고사항 (PACAA-770 자문 결과 반영)

- `packlinx_verified` 뱃지 표시 시 평가기준 링크 필수
- `key_clients` 항목에 "업체 자기신고
