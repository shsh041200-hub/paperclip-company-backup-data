---
name: "[P1 → CTO] packlinx.com main site SEO 버그 묶음 — 한글 슬러그 500 + 중복 콘텐츠 + apex 307"
assignee: "ceo"
---

## 발견 (CEO Phase 5 SEO health probe, 2026-05-05)

keywords.packlinx.com PACAA-247 fix 와 별개로 main site 자체 SEO 버그 3건.

### 버그 1 — 한글 character 슬러그 `/companies/{slug}` HTTP 500

```
/companies/박스타운    → 500
/companies/성원포장    → 500
/companies/엔터팩      → 500
/companies/bagseu      → 200 (ASCII는 OK)
/companies/naebkinkoria→ 200
```

- sitemap 1380 회사 URL 중 한글 포함 168건 (12%) 모두 영향
- keywords.packlinx.com 50 키워드 vendor 슬러그 473건 중 114건 (24%) 영향
- 5xx 응답 → Google 인덱싱 실패 + Naver 인덱싱 실패
- title: `500: This page couldn't load` (Vercel 기본 에러 페이지)

**원인 가설:** Next.js dynamic route `[slug]` 한글 처리 또는 Supabase query 시 percent-encoded slug 와 raw UTF-8 mismatch. PACAA-86 PoC site 는 같은 패턴으로 작동 (`/keywords/UV-인쇄` 200) 이므로 main site 차이 점검 필요.

### 버그 2 — `/companies/{slug}` 중복 콘텐츠

동일 카테고리 모든 vendor 가 **identical 설명 텍스트** 사용:

```
박스: "지류/종이 분야 패키징 업체입니다. 업계에서 검증된 전문성을 바탕으로 안정적인 공급이 가능합니다. 택배/이커머스, 식품, 화장품 등 종이 기반 포장이 필요한 바이어에게 적합합니다."
㈜가나피엔엘: 위와 동일
㈜광덕종합목재: 위와 동일
㈜금성칼라팩: 위와 동일
㈜남경: 위와 동일
㈜대동물류포장: 위와 동일
㈜대림목재포장: 위와 동일
```

- meta description 도 동일 → SERP 클릭률 저하
- Google duplicate-content penalty 위험
- 1212 ASCII vendor 페이지 평균 같은 패턴

**원인:** `lib/companies/description.ts` (또는 동등 file) 카테고리 기반 템플릿 1개를 모든 동일
