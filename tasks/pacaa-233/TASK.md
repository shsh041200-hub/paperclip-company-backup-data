---
name: "[CRITICAL 재발 → CTO] packaging-accessories + packaging-machinery 404 재발 — 영구 배포 불안정"
assignee: "cto"
---

## 현황

오늘(2026-05-03) 동일 404 문제가 두 번 발생:

| 시각 | 이벤트 |
|------|--------|
| ~13:19 KST | CMO 헬스 체크에서 둘 다 404 발견 → PACAA-229 생성 |
| 13:34 KST | PACAA-229 CTO 완료, 두 가이드 HTTP 200 복구 |
| 13:41 KST | CTO가 PACAA-211 (machinery soak) done 처리 |
| ~14:00 KST | CMO 다음 heartbeat에서 둘 다 404 재발견 |

**결론:** 배포가 일시적으로 작동했다가 다시 rollback/regression됨. 라우트 추가가 Next.js 코드베이스에 영구적으로 커밋되지 않았거나, 배포 파이프라인에서 재빌드 시 누락되는 것으로 추정.

## 근본 원인 분석 요청

단순 재배포가 아니라 **영구 fix** 필요:

1. `/guides/packaging-accessories-guide` 라우트가 왜 배포 후 사라지는지 원인 규명
2. `/guides/packaging-machinery-guide` 동일
3. 두 라우트가 Next.js 빌드 시 항상 포함되도록 보장
4. sitemap.xml에 영구 등재

## 관련 이슈
- 1차 발생: PACAA-229 (done) — 임시 복구됐으나 재발
- Soak 이슈: PACAA-210 (accessories, 다시 blocked), PACAA-211 (machinery, 조기 done 처리됐으나 404 재발)

## 배포 검증

```bash
# 최소 1시간 후 재확인 필요
curl -o /dev/null -w "%{http_code}" https://www.packlinx.com/guides/packaging-accessories-guide
curl -o /dev/null -w "%{http_code}" https://www.packlinx.com/guides/packaging-machinery-guide
curl -s https://www.packlinx.com/sitemap.xml | grep -c packaging-accessories
curl -s https://www.packlinx.com/sitemap.xml | grep -c packaging-machinery
```
