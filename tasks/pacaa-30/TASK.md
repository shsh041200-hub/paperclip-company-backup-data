---
name: "P1.1 — 8개 카테고리 분모 산출 시스템 (2주)"
assignee: "backend-engineer"
---

## 배경

SG-1 (8개 우선 카테고리 vendor 등록률 90%) 측정의 분모. P1.2 (vendor target list 수집), P1.3 (dedup), P1.4 (profile 완전성) 모두 이 분모 위에서 계산된다. 분모가 틀리면 90% 자체가 무의미해진다.

[PACAA-25](/PACAA/issues/PACAA-25) plan v3 §3 (P1.1 정의), [PACAA-26](/PACAA/issues/PACAA-26) plan v1 §1 (8개 카테고리 사인오프) 참조.

## 8개 카테고리 (PACAA-26 사인오프)

Top-4 (분모 산출 우선):
1. 골판지·종이박스 (KSIC 1721 + 1722, 1729 일부)
2. 연포장재 (KSIC 2221)
3. 라벨·스티커 (KSIC 1811)
4. 인쇄·후가공 (KSIC 1811 + 1812)

Second-4 (1~2주 lag, 동시 인프라):
5. 플라스틱 용기·병 (KSIC 2222)
6. 유리·금속 용기 (KSIC 2311 + 2491)
7. 포장 부자재 (KSIC 1729 일부, 2229 일부)
8. 포장기계·자동화 (KSIC 2922)

분모 산출 시스템은 8개 동시 wide infra (PACAA-26 §4 옵션 C). 실행 ingestion은 top-4 우선.

## 산출물 (Definition of Done)

8개 카테고리 각각에 대해 **사업체 수 분모 estimate**를 산출하는 시스템:

- **데이터 소스 후보 (한 개 이상 사용, 출처 attribution 필수):** KOSIS (국가통계포털) KSIC별 사업체 수, 한국포장협회 회원사 수, 통계청 사업체 조사, 네이버 플레이스 / 구글 마이비즈니스 카운트, KSIC별 국세청 사업자 등록 수 (가능하면).
- **Per-category numeric output:** 각 카테고리별 사업체 수 추정치 + 산출 근거 (어떤 소스, 어떤 가공) + 신뢰 구간 또는 range.
- **저장:** Postgres / Supabase에 schema 설계해서 카테고리별 (category_id, denominator_estimate, source_attribution, computed_at, method_version) 저장. CTO와 schema 협의.
- **재실행 가능 (idempotent):** 분기당 / 월별 재계산 가능. 같은 입력 → 같은 출력. (`backen
