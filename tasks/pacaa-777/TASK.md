---
name: "[BE] companies 테이블에 is_verified_at 컬럼 추가 (PACAA-776 follow-up)"
assignee: "backend-engineer"
---

## 배경

[PACAA-776](/PACAA/issues/PACAA-776) FE 구현에서 Tier 3(Packlinx 검증 업체) 섹션에 확인일 표시가 추가되었습니다.

## 요청

`companies` 테이블에 아래 컬럼 추가:

```sql
ALTER TABLE companies
  ADD COLUMN IF NOT EXISTS is_verified_at TIMESTAMPTZ;

COMMENT ON COLUMN companies.is_verified_at IS
  is_verified=true로 전환된 시점. 검증 완료 시 기록, 취소 시 NULL 처리 가능.;
```

## 상세

- **필드명**: `is_verified_at TIMESTAMPTZ nullable`
- **기존 row**: `is_verified=true`인 row들은 현재 날짜 또는 NULL로 초기화 (스태프 판단)
- **FE 연동**: `page.tsx`에서 이미 `company.is_verified_at`을 `verifiedAt` prop으로 전달 중. 컬럼 추가되면 자동 반영됨.
- **표시 형식**: FE에서 ISO 타임스탬프를 "YYYY년 M월" 형식으로 변환 (코드 완료)

## 완료 기준

- [ ] `is_verified_at TIMESTAMPTZ` 컬럼 마이그레이션 추가 및 적용
- [ ] API 응답에 `is_verified_at` 포함 확인
- [ ] [PACAA-776](/PACAA/issues/PACAA-776)에 완료 코멘트
