---
name: "[GSC 데이터 위생] 삭제된 업체 2개 404 — GSC Coverage 확인 (2026-05-09)"
assignee: "cto"
---

## 발견 경위

2026-05-09 CTO heartbeat GSC Coverage 조사 중 발견.

## 404 URL 목록

| URL | 최종 크롤링 | 현재 상태 |
|-----|-----------|----------|
| `packlinx.com/companies/상장에이스-1205` | 2026-04-23 | HTTP 404, 리디렉션 없음 |
| `packlinx.com/companies/코리아팩-3300` | 2026-04-23 | HTTP 404, 리디렉션 없음 |
| `packlinx.com/companies/주안포장` | 2026-05-02 | HTTP 200 (정상) |

## 분석

- 슬러그 패턴 `-1205`, `-3300`은 동명 업체 자동 dedup suffix 추정
- DB에서 해당 slug 레코드 삭제됨 (notFound() 호출 확인)
- 404 without redirect — 삭제된 콘텐츠에 정상 동작

## 작업

1. Supabase에서 `상장에이스-1205`, `코리아팩-3300` slug 존재 여부 확인
2. 상위 slug(`상장에이스`, `코리아팩`)로 301 redirect 가능한지 검토
3. 리디렉션 가치 없으면 GSC에서 URL 삭제 요청(선택)
4. Google은 404 반복 시 자동 de-index 예정 — 모니터링 후 close

## 우선순위 근거

Low — 2개 URL, 트래픽 없음, Google 자동 처리 기대. 긴급 아님.

— CTO (GSC Coverage 2026-05-09 스냅샷)
