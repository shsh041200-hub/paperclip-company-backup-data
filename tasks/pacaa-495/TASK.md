---
name: "PACAA-490 CMO r3 brief — 메인페이지 벤치마킹 + 10 컨셉 명세 (FE implement 선행)"
assignee: "cmo"
---

## Context

부모: PACAA-490. 보드 directive (PACAA-493 c7899cf9):

> 메인페이지 구조에 대한 벤치마킹을 좀 더 해봐 그리고 개선안 10개를 만들어서 크롬으로 너가 알아서 내가 보기 쉽게 창을 띄워놓고 내가 그중 하나를 고르면 그 하나를 제외하고서는 나머지 것들은 전부 삭제하면돼 잔여 파일이나 코드가 안남게

현재 v3 (Sidebar Directory) = 보드 view 상 "카테고리 페이지 안에 들어온 느낌" — 메인페이지답지 않음 판정. r1 (3-direction) → r2 (v1/v2/v3) 거쳐 r3 (10 variant) 으로 회전.

## 작업 범위 (CMO brief only, 코드 0)

### 1. 벤치마킹 (B2B SaaS / 검색·디렉토리 / 한국 B2B 메인 — 5~7개 정성 분석)

권장 후보 (CMO 자율 추가 가능):
- Stripe homepage (B2B SaaS 정석)
- Linear (단정한 B2B + 다크 hero)
- Vercel (B2B 인프라 + 카드 그리드)
- Notion (B2B SaaS + 다층 IA)
- Anthropic / OpenAI (research 톤)
- 한국 B2B: 토스플레이스, 채널톡, 잔디 (한글 카피·정보 밀도)
- 검색·디렉토리 본질 동종: Yelp business, Houzz, ThomasNet

분석 axes:
- Hero shape (full-bleed / split / search-prominent / minimal)
- 1차 IA (검색 / 카테고리 / 컨텐츠 / 사용 사례)
- Data surface (vendor 카드 / 통계 / 컨텐츠 카드 / 빈 grid)
- CTA 패턴 (search-first / signup / contact / browse)
- Tone (formal / friendly / techy / minimal)

### 2. 10 컨셉 명세서 (Markdown)

각 컨셉에 대해:
- 컨셉명 (1줄, 한국어, 패턴 명시)
- Hero pattern (벤치 reference + axes 매핑)
- 1차 IA (어떤 데이터·기능을 hero 다음에 surface)
- 2차 IA (그 아래 섹션 순서)
- CTA 위치·문구 (검색-first / browse-first / contact-first)
- 차별점 (다른 9개와 구분되는 1줄)
- FE 난이도 (low / mi
