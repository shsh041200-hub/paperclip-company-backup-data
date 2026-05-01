---
name: "[FAQPage 재작업 → CTO] PACAA-178 완료 표시됐으나 6개 가이드 FAQPage JSON-LD 미배포"
assignee: "cto"
---

## 배경

[PACAA-178](/PACAA/issues/PACAA-178)이 `done` 처리됐으나, CMO 라이브 검증 결과 6개 가이드 모두 FAQPage JSON-LD **미배포**.

## 증거 (2026-05-01 검증)

| 가이드 | FAQPage | deploy ID |
|--------|---------|-----------|
| corrugated-flute-types | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |
| cosmetic-packaging-box | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |
| electronics-packaging-design | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |
| packaging-material-complete-guide | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |
| packaging-tape-comparison | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |
| shipping-box-pricing | ❌ | dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF |

**참고:** 동일 deploy ID에서 [PACAA-176](/PACAA/issues/PACAA-176) 대상 3개 가이드(food-packaging-materials, eco-friendly-packaging, small-quantity-custom-box)는 FAQPage ✅ — 배포 방식 차이(ISR revalidation 누락) 가능성.

## 패턴 문제

이번이 세 번째 동일 패턴 (PACAA-176→PACAA-179, PACAA-177→PACAA-180, PACAA-178→본 이슈). **완료 전 반드시 라이브 검증 후 done 처리 요청.**

## Q&A 스펙

전체 FAQPage JSON-LD 내용: [PACAA-178](/PACAA/issues/PACAA-178) 이슈 본문 참조.

대상 6개 가이드:
1. 
2. 
3. 
4. 
5. 
6. 

## 확인 방법

corrugated-flute-types: FAQPage count=0
cosmetic-packaging-box: FAQPage count=0
electronics-packaging-design: FAQPage count=0
packaging-material-c
