---
name: "[BE] PACAA-622 후속 — naver_local 465건 website enrichment"
assignee: "backend-engineer"
---

## 배경

[PACAA-622](/PACAA/issues/PACAA-622) (CEO own) — 보드가 `daf6d5c5` 인터랙션 `both` 선택 → naver_local 소스 vendor 465건 website URL enrichment 발의.

[PACAA-623](/PACAA/issues/PACAA-623) read-only 분석: naver_local 760건 중 465건 (61.18%) website 누락.

## 작업

1. **Source:** vendor_candidates 테이블 `data_source='naver_local' AND website IS NULL` (예상 465건).
2. **방법:** Naver Local API (이미 ENV 에 인젝션된 NAVER_CLIENT_ID/NAVER_CLIENT_SECRET 활용. PACAA-95 Phase B 패턴 참고).
3. **per-vendor 절차:**
   - 회사명 (`name`) + 카테고리 또는 주소 fragment 로 Naver Local 검색
   - 첫 match 의 `homepage` 필드 추출
   - 빈 / 무효 (http(s) 스킴 X) skip
   - validated URL 만 `vendors.website` UPDATE (commit)
4. **Rate limit:** Naver Local API quota 일일 25k req (예상 sufficient). 1 req/vendor + retry budget.
5. **idempotency:** 이미 website 있는 vendor 는 skip (`WHERE website IS NULL`).

## Acceptance

- [ ] BE 가 enrichment 스크립트 작성 + dry-run 카운트 보고 (PACAA-622 코멘트).
- [ ] CEO accept 시 실 mutation 실행.
- [ ] 결과 카운트: 매치 N / no-match M / total 465.
- [ ] vendors 테이블 N 행 website 업데이트.
- [ ] PACAA-622 cross-link 코멘트 (associated PACAA-### enrichment ship).

## Reversibility

Two-way: `vendors.website` UPDATE 는 SQL 복구 가능 (audit trail 보존). dry-run 단계 0 mutation.

## 출처
