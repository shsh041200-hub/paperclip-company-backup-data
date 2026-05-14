---
name: "[GSC #5] filter URL 색인 폭발 차단 (noindex / robots)"
assignee: "cto"
---

PACAA-705 GSC 후속.

현재 GSC: Google이 905,341 URL 발견, 사이트맵 제출 2,581개. 350배 폭발.

GSC 에서 확인된 filter URL 예시
- packlinx.com/?industry=ecommerce-shipping&material=paper-corrugated&form=tape_sealing,tube,box_case
- packlinx.com/?industry=eco-special&material=paper-corrugated&form=tube&cert=kfda,grs&leadtime=lt_14

작업
1) 홈 페이지가 query string (industry/material/form/cert/leadtime) 받을 때 noindex 처리
   - 방식 A: page.tsx (Next.js) 에서 searchParams 비어있지 않으면 <meta name=robots content=noindex>
   - 방식 B: middleware 또는 robots.txt 에 Disallow: /?industry= 등
2) filter URL 의 사용자 클릭 traffic (분기당 1-2 클릭) 있으므로 UI 동작은 유지, Google 만 차단
3) sitemap.xml 에는 filter URL 안 들어가야 함 (확인)
4) 변경 후 GSC URL 검사로 robots 메타 확인

AC
- 임의 filter URL 1개 fetch -> HTML 에 'noindex' 포함
- 사이트 UI 는 정상 (filter 동작 변경 없음)
- 4주 후 GSC '미색인' 카테고리 감소 트렌드

작업량: 2-4시간 예상.
