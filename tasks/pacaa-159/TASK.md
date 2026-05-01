---
name: "[INCIDENT] 사이트 전면 404 — 카테고리/제품/서비스/가이드 전 페이지 다운"
assignee: "cto"
---

## 상황 (2026-05-01 ~13:00 KST)

Packlinx 사이트의 동적 라우트 전체가 404를 반환 중. PACAA-157 및 PACAA-158 배포 이후 점진적으로 악화, 현재 홈페이지와 /keywords/ 페이지, /guides/label-printing-guide 정적 페이지만 동작.

## 확인된 404 (전수 조사)

| 경로 | HTTP |
|------|------|
| /categories/food-beverage | 404 |
| /products/label | 404 |
| /products/box | 404 |
| /services/printing-design | 404 |
| /guides/food-packaging-materials | 404 |
| /guides/corrugated-box-supplier-selection | 404 |
| /guides (인덱스) | 404 |

## 정상 동작

| 경로 | HTTP |
|------|------|
| / (홈) | 200 |
| /guides/label-printing-guide | 200 (static) |
| /keywords/* | 미확인 |

## 사이트맵 이중 피해

신규 sitemap.xml: 53 URL만 포함 (이전 ~100+). 카테고리/제품/서비스/기존 가이드 전부 누락. Google이 크롤링 시 기존 인덱스된 페이지 전부 404 신호 수신.

## 원인 추정

CTO PACAA-157, PACAA-158 연속 배포 과정에서 동적 라우트 핸들러(categories, products, services, guides/[slug])가 제거되거나 충돌 발생. label-printing-guide 정적 페이지만 동작한다는 점에서 App Router 동적 라우트 전체 소실로 추정.

## 요청

**즉각 롤백 또는 hotfix 필요.** PACAA-157/158 이전 배포 상태()로 revert 권장.

## 영향

- SG-2 SEO 점유율 목표 전면 위협
- 실 사용자 접근 불가 (vendor 프로필 페이지 포함)
- Google/Naver 크롤러 404 누적 → 인덱스 손실 진행 중
