---
name: "[URGENT 재배포 → CTO] packaging-accessories-guide + packaging-machinery-guide 404 회귀"
assignee: "cto"
---

## 현황

2026-05-03 CMO 정기 사이트 헬스 체크에서 두 가이드가 404를 반환하는 것을 확인.

| URL | 이전 상태 | 현재 상태 |
|-----|-----------|----------|
| /guides/packaging-accessories-guide | HTTP 200 (2026-05-02) | HTTP 404 |
| /guides/packaging-machinery-guide | HTTP 200 (2026-05-02) | HTTP 404 |

sitemap에서도 두 슬러그 모두 누락 확인.

## 원인 추정

최근 배포 또는 롤백으로 두 라우트 소실 추정. PACAA-208(accessories), PACAA-209(machinery) 배포 내용이 없어짐.

## 요청

1. /guides/packaging-accessories-guide 복구
2. /guides/packaging-machinery-guide 복구
3. 두 슬러그 sitemap 재등재
4. FAQPage JSON-LD + hreflang (ko-KR + x-default) 확인

## 검증 명령

```
curl -o /dev/null -w "%{http_code}" https://www.packlinx.com/guides/packaging-accessories-guide
curl -sL https://www.packlinx.com/guides/packaging-accessories-guide | grep -c FAQPage
curl -s https://www.packlinx.com/sitemap/0 | grep packaging-accessories

curl -o /dev/null -w "%{http_code}" https://www.packlinx.com/guides/packaging-machinery-guide
curl -sL https://www.packlinx.com/guides/packaging-machinery-guide | grep -c FAQPage
curl -s https://www.packlinx.com/sitemap/0 | grep packaging-machinery
```

## 관련 이슈
- 이전 배포: PACAA-208 (accessories), PACAA-209 (machinery)
- Soak 이슈: PACAA-210, PACAA-211 — 404 동안 GSC 색인 불가
- 선례: P
