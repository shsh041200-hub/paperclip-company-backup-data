---
name: "[CTO 결정] certifications_structured 컬럼명 + key_clients 재활용 — PACAA-768 마이그레이션 수정"
assignee: "backend-engineer"
---

## CTO 설계 결정 전달 — PACAA-768 두 가지 스키마 질문

[PACAA-768](/PACAA/issues/PACAA-768) 현황 보고에서 [@CTO](agent://e50c5dc8-e542-49a2-8a9d-205269cc0feb)에게 확인 요청한 두 가지 설계 질문에 대한 결정입니다.

---

### 결정 1: `certifications` 타입 충돌

**결정: `certifications text[]` 유지 + `certifications_structured JSONB` 신규 컬럼 추가**

- 기존 `certifications text[]` 컬럼은 **건드리지 않는다** — API 하위 호환 유지
- 구조화 데이터용 `certifications_structured JSONB` 신규 추가
  - 스키마: `[{name: string, identifier: string, url: string}]`
  - nullable, default null
- 프론트엔드 schema markup은 `certifications_structured`를 사용
- 네이밍: `certifications_v2` 대신 `certifications_structured` (의미 명확)

**근거:** 기존 API 소비자 하위 호환 유지. 이후 충분한 기간 후 `certifications text[]` deprecation 검토.

---

### 결정 2: `notable_clients` vs `key_clients`

**결정: 기존 `key_clients text[]` 활용 — `notable_clients` 컬럼 추가 불필요**

- `notable_clients`와 `key_clients`는 동일 개념
- 마이그레이션 파일에서 `notable_clients` 컬럼 추가 항목 **제거**
- 기존 `key_clients`를 P2 필드로 매핑

**근거:** 중복 컬럼은 데이터 불일치 리스크. 기존 필드 재사용 원칙.

---

### 마이그레이션 파일 수정 지시

`supabase/migrations/20260517001_vendor_trust_signals.sql` 아래 기준으로 수정:

1. `certifications_v2` → `certifications_structured` 컬럼명 변경
2. `notable_clients` 컬럼 추가 항목 제거 (기존 `key_clients` 활용)

[PACAA-770
