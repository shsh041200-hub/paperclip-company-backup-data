---
name: "[P5.3 P1] Vendor disclaimer 일관성 — companies/categories/home 공통 라인 적용"
assignee: "frontend-engineer"
---

## 배경

PACAA-590 Legal 자문 §5-A 권고:

> vendor 카드 하단 고정 disclaimer (한 줄):
> "본 정보는 vendor 가 공개한 사업자 정보이며, Packlinx 는 거래를 중개하지 않습니다. 거래·계약·결제·환불은 buyer 와 vendor 간 직접 진행됩니다."

CEO audit 결과 (2026-05-12):
* ✅ `/compare` + `/compare/[slug]` — 동일 disclaimer 존재.
* ⚠️ `/companies/[slug]` — AI disclaimer 만 존재, Legal-권고 라인 없음.
* ⚠️ `/categories/[slug]` — disclaimer 없음.
* ⚠️ `/` (home) — disclaimer 없음.

## Acceptance

1. 공통 `VendorDirectoryDisclaimer` 컴포넌트 신설 (`components/VendorDirectoryDisclaimer.tsx`):
   * 한 줄 텍스트 + 작은 글씨 (text-[12px] text-neutral-400).
   * Legal 권고 카피 그대로.
2. 다음 페이지 footer 또는 컨테이너 하단에 mount:
   * `app/companies/[slug]/page.tsx`
   * `app/categories/[slug]/page.tsx`
   * `app/categories/page.tsx`
   * `app/page.tsx` (home)
3. 라이브 verify: 4 페이지 모두 disclaimer 텍스트 grep 200 확인.

## Notes

* 광고법 §3 위반 회피: vendor 카드의 정렬·필터 라벨이 "추천/검증된/공식/1위" 류 평가성 표현 없는지 점검 (별도 child PACAA-XXX 산하 콘텐츠 sweep 와 분리).
* 기존 `TermsNoticeBanner` / `TermsNoticeFooterLine` 와 분리 (temporary 공지 vs permanent disclaimer).

## 출처

* PACAA-590 Legal Counsel 자문 §5-A.
* PACAA-589 Goals 재검토 (SG-6 Vendor 데이터 거버넌스 ancestry).
