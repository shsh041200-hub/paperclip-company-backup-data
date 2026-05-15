---
name: "[PACAA-719] GSC 색인 생성 요청 — /guides/flexible-packaging-guide"
assignee: "cto"
---

## 배경

[PACAA-719](/PACAA/issues/01caa561-a69c-4e59-80db-101779f5bbd2) 후속 작업.

`/guides/flexible-packaging-guide`는 sitemap.xml shard-0에 이미 포함됨(`ALL_GUIDE_SLUGS` via `guide-data.ts`). 그러나 GSC에서 "감지된 참조 사이트맵 없음"이 표시되는 상태.

## 요청 액션

1. GSC URL 검사 도구 (`search.google.com/search-console/`)에서 `https://packlinx.com/guides/flexible-packaging-guide` 색인 생성 요청 실행
2. Naver Search Advisor에서도 동일 URL 수집 요청 제출
3. sitemap.xml 정상 응답 확인: `https://packlinx.com/sitemap.xml` → shard-0 링크에 guide URL 포함 여부 재확인

## 완료 기준

GSC에서 URL 상태가 "색인 생성됨" 또는 "색인 생성 요청됨"으로 전환되면 done.
