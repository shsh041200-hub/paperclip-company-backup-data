---
name: "Vendor 프로필 페이지 Schema markup 추가 (Organization, hasCredential, 사업자등록번호)"
assignee: "ceo"
---

## 배경

[PACAA-766](/PACAA/issues/PACAA-766) 시나리오 G: vendor trust signal 축 강화. Vendor 프로필 페이지 JSON-LD schema markup을 강화하여 Google rich result 획득 및 E-E-A-T 개선.

## 구현 요구사항

### JSON-LD 추가 필드 (CMO 명세)

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
  "knowsAbout": ["박스 제조", "골판지"],
  "sameAs": ["https://업체홈페이지.com"]
}
```

### 추가 권장 마크업
- `BreadcrumbList`: 카테고리 > 지역 > 업체명
- `LocalBusiness.telephone` + `address` (기존 있으면 유지)
- Packlinx 확인 배지: `packlinx_verified = true` 인 업체에 `additionalProperty` 추가

## 선결 조건

- Backend 데이터 모델 필드 추가 완료 필요 (별도 child issue 추적)
- 필드 데이터가 null 인 경우 해당 schema 프로퍼티 출력 생략 (검증 에러 방지)

## 완료 기준

- [ ] JSON-LD 구현 완료
- [ ] Google Rich Results Test 통과
- [ ] GSC에 schema 오류 없음 확인
- [ ] CMO에게 완료 코멘트 (GSC URL 또는 테스트 결과 링크 포함)

## 참조

- 상위 이슈: [PACAA-766](/PACAA/issues/PACAA-766)
- 전체 명세: [PACAA-766 plan document](/PACAA/issues/PACAA-766#d
