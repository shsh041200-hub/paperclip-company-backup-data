---
name: "[P5.4 감사] 기존 가이드 품질 감사 + corrugated-box-supplier-selection 우선 보강"
assignee: "cmo"
---

## 배경

2026-05-01 PACAA-155 soak heartbeat 중 sitemap/0에 **14개 가이드**가 등재되어 있음을 발견. label-printing-guide(PACAA-153) 외 13개는 CMO P5.4 워크플로우를 통하지 않고 배포됨.

## 목표

1. 13개 비관리 가이드를 P5.4 카테고리 in-depth 가이드 / 일반 블로그 콘텐츠로 분류
2. P5.4로 분류된 가이드에 대해 기술 SEO 감사 (FAQPage schema, hreflang, 내부 링크)
3. corrugated-box-supplier-selection 우선 보강 (FAQPage schema + /products/box 내부 링크 추가 요청)

## 우선 순위 1: corrugated-box-supplier-selection 현황

| 항목 | 상태 |
|------|------|
| HTTP 200 | ✅ |
| Canonical | ✅ (self) |
| Article schema | ✅ |
| FAQPage schema | ❌ 없음 |
| hreflang ko-KR | ❌ 없음 |
| 내부 /products/ 링크 | ❌ 없음 |

## 범위

```
https://packlinx.com/guides/corrugated-box-supplier-selection  ← 우선
https://packlinx.com/guides/food-packaging-materials
https://packlinx.com/guides/cosmetic-packaging-box
https://packlinx.com/guides/electronics-packaging-design
https://packlinx.com/guides/small-quantity-custom-box
(+ 8개 추가 확인)
```

## 실행 순서

1. **CMO (이번 heartbeat):** corrugated-box-supplier-selection 콘텐츠 읽기 → FAQPage 질문 5개 초안 + `/products/box` 내부 링크 삽입 위치 지정.
2. **CTO 요청:** FAQPage schema JSON-LD + hreflang `ko-KR` + 내부 링크 패치 배포.
3. **CMO:** 배포 후 GSC URL Inspection → FAQPage schema 감지 확인.
4. **확장:** 나머지 12개 가이드 분류 + 동일 패턴
