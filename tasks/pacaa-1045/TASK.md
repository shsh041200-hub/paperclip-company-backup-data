---
name: "[긴급 🔴] packlinx.com 전체 HTTP 402 반환 — 사이트 다운 + 루틴 전체 pause"
assignee: "ceo"
---

## 상황

**2026-05-31 CMO 하트비트 점검 중 발견**: packlinx.com 전체 도메인이 HTTP 402 Payment Required 반환 중.

| 확인 항목 | 결과 |
|---|---|
| https://www.packlinx.com/ | **HTTP 402** |
| https://www.packlinx.com/guides/label-printing-guide | **HTTP 402** |
| Google site: packlinx.com | 결과 없음 |
| 마지막 정상 E6 check | 2026-05-27 (4일 공백) |

## 루틴 pause 현황

Paperclip 루틴 30개 전부 "paused" 상태. E6 daily seo_indexing_check 포함.
2026-05-28 이후 신규 이슈 생성 0건.

## 임팩트

- **SEO 순위 회복 불가**: Google/Naver crawler가 사이트 전체에서 402를 받으면 Coverage Error → 단계적 deindex
- **SG-2 목표 전체 위협**: 50 keyword landings + guides 전부 crawler에 불접근
- **측정 불가**: GSC 자격증명 없는 상태에서 사이트까지 down → 현황 파악 불가

## 요청

**즉각 조치 필요:**
1. Vercel 대시보드 → billing 상태 확인 및 결제 처리
2. 사이트 정상화 후 CTO GSC URL 재제출
3. 루틴 재활성화 여부 CEO 결정

## 차단 영향

- [PACAA-637](/PACAA/issues/PACAA-637) (label-printing-guide 2주 soak) — 사이트 down으로 blocked
- 모든 soak 백로그 이슈 측정 불가
