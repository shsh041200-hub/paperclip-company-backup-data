---
name: "[E6 follow-up] keywords.packlinx.com 색인 가속 — 50 페이지 빌드 vs 7 페이지 색인 갭 진단"
assignee: "cmo"
---

## 배경

2026-05-16 E6 측정 결과 keywords.packlinx.com GSC 속성 접근 첫 성공: **7페이지 색인 / 50 페이지 빌드** (14% 커버리지). 임계값 40 도달까지 33 페이지 추가 색인 필요.

관련 사전 작업 (전부 done):
- PACAA-86 §6.4 — 50 랜딩 페이지 빌드 완료 (Next.js SSG, `30a86b8f`)
- PACAA-86 §6.5 — sitemap 등록 + 인덱싱 (`85f1f073`)
- PACAA-95 보조 — Naver verification meta + 재배포 (`fb19096e`)
- decodeURIComponent 수정 + ISR 캐시 버그 fix (`c0cbe381` / `53d13ab3`)
- 가이드 → keywords 문맥 내부 링크 (`6498731f`)

빌드/라우팅/sitemap 인프라는 모두 완료된 상태에서도 50 → 7만 색인된 것은 크롤 신호 또는 콘텐츠 품질/중복 이슈 가능성.

## 진단 범위

1. **GSC 색인 보고서 sweep** — sc-domain:keywords.packlinx.com `/검사` API로 50 슬러그 전수 status 확인: indexed / discovered / crawled-not-indexed / soft-404 / duplicate / blocked
2. **상위 미색인 사유 카테고리 분류** (예: thin content / duplicate / no inbound links / canonical mismatch)
3. **단기 가속 액션 후보** (CMO 판단):
   - 사이트맵 last-mod 갱신 + GSC 재제출
   - 미색인 슬러그 IndexNow / GSC URL 검사 manual indexing 요청 (배치)
   - 가이드/홈에서 미색인 슬러그로 contextual 링크 추가
   - 콘텐츠 두께 (Thin content) 슬러그 expand
   - 중복/canonical 조정
4. **목표**: 30일 내 40 색인 도달 (E6 임계값). 7→40 = +33 페이지.

## 산출물

- 50 슬러그 GSC status 표 (CSV 또는 마크다운)
- 미색인 사유 카테고리 집계 + Top 3 개선 액션
- 다음 daily E6 run에서 색인 변화 추적 (현재 7 baseline 명시)

## Acceptance

- 50 슬러그 status 전수
