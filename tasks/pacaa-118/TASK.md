---
name: "P1.C Slug 정규화 — vendor import 충돌 해결 + 185 -NNNN 정리"
assignee: "ceo"
---

PACAA-115 산하 child C.

## 진단
현재 906 vendor 중 185개 (20%) 가 `-NNNN` 숫자 suffix slug. import 단계에서 slug 충돌 시 임의 숫자를 붙여 회피한 흔적. 의미성 0, dedup 신호 없음.

## 작업
1. Vendor import 정규화 로직: slug 충돌 시 `-NNNN` 대신 의미 있는 식별자 (지역 코드 / 사업자등록번호 마지막 4자리 / 카테고리 prefix) 사용. 정책은 import 모듈 README 에 명시.
2. 기존 185개 `-NNNN` slug:
   a. 같은 base slug 끼리 group → 신뢰도 점수 (등록 정보 완전성·연락처 검증·최근 update) 로 단일 canonical 선정.
   b. 비-canonical 변형 → 301 redirect 테이블 등록.
   c. canonical slug 가 의미 있는 식별자로 교체 가능하면 교체 + 구 slug 도 redirect.
3. Unit test: slug uniqueness 보장 + 의미성 (숫자만으로 끝나지 않음) 검증.
4. DB 쿼리 acceptance 검증.

## Acceptance
- [ ] DB: `WHERE slug ~ -[0-9]+$` 결과 0건
- [ ] 185 redirect 모두 `curl -I` 200/301 정합
- [ ] import unit test 통과 (충돌·의미성)

## Reversibility
Two-way (slug 변경은 redirect 로 복원 가능). SEO 4–6주 reprocess 비용은 A 와 통합 산정.

## 의존성
A 의 canonical 정책 확정. Backend Engineer 복구 시 위임 강력 후보 (vendor pipeline 영역).
