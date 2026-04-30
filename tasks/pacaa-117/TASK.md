---
name: "P1.B Sitemap 1,000-cap 해제 + sitemap-index 분할"
assignee: "backend-engineer"
---

PACAA-115 산하 child B.

## 진단
현 sitemap 1,031 URL, 실제 vendor ≥1,200 (PACAA-114 lib probe 906 + 누락 ≥200). 단일 sitemap.xml 의 SELECT/LIMIT 또는 generator 의 hard cap 추정.

## 작업
1. Sitemap 생성 코드의 LIMIT/cap 식별 + 제거. 50,000-URL/sitemap, 50MB/file (Google 한도) 초과 시 sitemap-index 자동 분할.
2. URL 출력은 ADR (PACAA-115.A) 의 raw UTF-8 정책 따름.
3. `lastmod`: vendor row 의 `updated_at` 와 일치하는지 검증 (vendor 정보 변경 시 자동 갱신).
4. DB 카운트 vs sitemap URL 카운트 일치 자동 검증 스크립트 (CI 또는 cron 후 alert).
5. GSC sitemap.xml 재제출.

## Acceptance
- [ ] sitemap.xml URL 수 ≥ DB vendor 수 (정확히 일치, ±0)
- [ ] sitemap-index 동작 (>50k 대비)
- [ ] lastmod 변경 테스트 (vendor update → sitemap lastmod 변동)
- [ ] GSC re-submit 완료

## Reversibility
Two-way. cap 를 코드에서 다시 끼울 수 있음. 가역.

## 의존성
A 의 canonical 정책 확정 후 진행 (URL 형식 의존). Backend Engineer 복구 시 위임 후보.
