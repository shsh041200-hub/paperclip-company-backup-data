---
name: "[BE] PACAA-622 후속 — association 264건 website enrichment"
assignee: "backend-engineer"
---

## 배경

[PACAA-622](/PACAA/issues/PACAA-622) (CEO own) — 보드가 `daf6d5c5` 인터랙션 `both` 선택 → association 소스 vendor 264건 website URL enrichment 발의.

[PACAA-623](/PACAA/issues/PACAA-623) read-only 분석: data_source = association 류 (한국포장협회 / 골판지조합 등 명단) 264건 website 누락.

## 작업

1. **Source:** vendor_candidates 테이블 `data_source LIKE 'association%' AND website IS NULL` (예상 264건. 정확한 source 종류 확인 필요).
2. **방법 (3 옵션, BE 분석 후 선택):**
   - **(a) 협회 디렉터리 직접 크롤:** 원본 source 페이지 재방문 → name 매칭 → website 추출.
   - **(b) Google CSE / 검색 lookup:** "회사명 site:.kr OR site:.co.kr" 첫 결과.
   - **(c) Naver 일반 검색 fallback:** name 으로 Naver 일반 검색 → 첫 도메인 매치.
3. **per-vendor 절차:**
   - name 정확 매칭 (퍼지 매칭 위험 → false-positive 회피).
   - 추출 URL validate (http(s) + DNS 해석 + 200 응답).
   - 매칭 confidence < 80% → skip.
4. **dry-run + 보드 sample 검수:** 처음 20건 dry-run 후 CEO + 보드 sample 검수 → bulk 실행 결정.
5. **idempotency:** `WHERE website IS NULL`.

## Acceptance

- [ ] BE 가 source 종류 + 카운트 라이브 verify 후 PACAA-622 코멘트 (264 정확성).
- [ ] 옵션 (a/b/c) 추천 + dry-run 20건 sample.
- [ ] CEO + 보드 검수 accept 시 bulk 실행.
- [ ] 결과 카운트: 매치 N / no-match M.
- [ ] vendors 테이블 N 행 website 업데이트 + PACAA-622 cross-link.

## Reversibility

Two-way (SQL UPDATE
