---
name: "P4b 사전 — 가이드/블로그 V04 적용 CMO 의견 (PACAA-463)"
assignee: "cmo"
---

## 범위 (Sub-Phase 4b CMO consultation)

**parent**: PACAA-463 / **plan**: `plans/PACAA-463/plan-v5-phase4.md`.

콘텐츠 라우트 (`app/guides/*` 6 페이지, `app/blog/*` 2 페이지) 는 V03 LINX Orange 톤. CEO 가 V04 (Stripe Purple) 토큰 적용 진행/보류 결정에 CMO 의견 필요.

### 질문 (코멘트로 응답)

1. **content brand 의도**: 가이드 6 페이지 + 블로그 2 페이지 V03 LINX Orange 톤 = 의도된 content brand voice 인가, legacy 잔존인가?
2. **V04 톤 영향 예측**: V04 Stripe Purple 적용 시 콘텐츠 신뢰성/전환율/SEO 직간접 영향 예상?
3. **A/B 단축 테스트 가능성**: 영향 불명확 시 가이드 1 페이지만 V04 → 1주 단축 데이터 (Vercel preview + GA) 후 결정 가능?

### 응답 후 흐름

* CMO **"V04 적용 OK"** → CEO 가 Sub-Phase 4b FE child 발의 (8 페이지 토큰 swap).
* CMO **"V03 보존"** → 본 issue done, Phase 4 = sub-4a 만 완료. 사이트 톤 일부 비균질 수용 (보드 보고).
* CMO **"A/B 테스트"** → CEO 가 단축 plan + FE child (가이드 1 페이지 + 측정 routine 발의).

## DoD

* CMO 코멘트 응답 (200~500자, 권장+이유).
* CEO 가 응답 받고 다음 단계 발의 시 본 issue done.

## 정보

* Phase 1-3 결과: 5 V04 라우트 (vendor/main/categories x2/products) 머지, 토큰 시스템 globals.css 박힘.
* 라이브 sample (V04 톤 어떤지): https://www.packlinx.com/companies/seoulpojang vs https://www.packlinx.com/guides/flexible-packaging-guide.
