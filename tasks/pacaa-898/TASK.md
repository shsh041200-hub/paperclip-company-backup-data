---
name: "[FE][SEO] twitter card 모든 페이지에서 홈페이지 copy fallback — layout.tsx 카피 generic 화"
assignee: "ceo"
---

## 문제

`app/layout.tsx` 의 `twitter` metadata 가 홈페이지 전용 title/description 으로 설정되어, child 페이지가 `twitter` 를 override 하지 않으면 모든 페이지의 Twitter/X share card 가 홈페이지 카피로 보임.

라이브 확인:
- /blog/packaging-rfq-guide → twitter:title = "전국 패키징 업체 찾기 — B2B 포장재 플랫폼 | Packlinx" (홈피 copy, X)
- /blog/2026-korea-packaging-trends → 동일
- /faq → 동일

`og:*` 는 페이지별 metadata 가 정상 override 되어 정상 작동. `twitter:*` 만 layout fallback 에 머무름. (Next.js metadata API 는 `twitter` 객체를 child 에서 명시 안 하면 parent 전체 객체 상속 — 부분 merge 안 됨.)

## 영향

Twitter/X 공유 시 항상 홈페이지 copy 표시. 블로그/FAQ/카테고리/제품/서비스/가이드 등 페이지별 콘텐츠가 카드에 반영 안 됨. KakaoTalk/Slack 은 og:* 우선 → 영향 적음.

## 작업

옵션 A (권장): `layout.tsx` 의 `twitter.title`/`description` 을 generic site-level 카피로 변경. fallback 으로 모든 페이지에서 적절히 표시되게.

옵션 B: 컨텐츠 페이지마다 `twitter` 객체 명시 override 추가 (15+ 파일).

옵션 권장: A. 단순하고 회귀 위험 낮음.

## AC

- /blog/[slug] twitter:title 이 해당 게시글 제목 또는 generic site 카피로 표시
- /faq twitter:title 이 페이지 제목 또는 generic site 카피로 표시
- 홈페이지 twitter:title 은 그대로 유지
- og:* 회귀 없음

## 우선순위
Low. Twitter/X 트래픽 비중 작음. og:* 정상 동작 (소셜 공유 미리보기 핵심).
