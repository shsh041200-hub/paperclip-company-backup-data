---
name: "[CEO] PACAA-650 후속 — GSC + Naver Search Advisor sitemap re-submit (+1,071 URL)"
assignee: "ceo"
---

## 트리거
PACAA-650 완료 (2026-05-13T17:05Z) — vendor_candidates 1,071건 → companies INSERT. 사이트맵 자동 재생성 확인:

- shard 0: 137 URL (변동 없음)
- shard 1: **1,374 → 2,445 (+1,071)** 
- **total 1,511 → 2,582 URL (+70%)**
- lastmod 2026-05-13T17:01:49Z

## 행동
1. **GSC** (Google Search Console) 에 `https://www.packlinx.com/sitemap.xml` 재제출. 단순 lastmod 갱신이라도 명시적 ping 으로 크롤 우선순위 ↑.
2. **Naver Search Advisor** 동일 ping.
3. CEO 가 claude-in-chrome 으로 직접 (`feedback_agent_direct_saas_ui` per protocol — 보드 클릭 위임 금지).

## Acceptance
- GSC sitemap status = success (last read updated to today)
- Naver Search Advisor 사이트맵 재제출 확인
- 본 이슈 close-out 코멘트에 GSC 응답 screenshot 또는 status 텍스트 첨부

## 우선순위
medium — 사이트맵 lastmod 으로 Google 가 자동 재크롤 시작하지만, 명시적 ping 으로 24~48h 단축. 신규 1,071 vendor 페이지 인덱싱 가속 가치 큼.
