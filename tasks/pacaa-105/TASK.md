---
name: "PACAA-95 보조 — Naver verification meta + 재배포"
assignee: "backend-engineer"
---

## Context
보드가 Naver Search Advisor에서 keywords.packlinx.com 사이트 추가하고 HTML meta 인증 토큰을 발급함 (PACAA-95 코멘트 ddb587a1).

## 산출물

1. site/app/layout.tsx Metadata 객체 verification 필드에 추가:
   verification: { other: { "naver-site-verification": "75a36acde7c07e0f3159476555830e66d1769d9a" } }
2. bash site/scripts/deploy-vercel.sh 로 production 재배포.
3. 검증: curl https://keywords.packlinx.com | grep naver-site-verification → 토큰 노출 확인.
4. 본 이슈 완료 코멘트 + PACAA-95 부모에 unblock 트리거.

## DoD
* meta 태그 production HTML <head> 에 노출
* 배포 alias 갱신 + URL 검증 결과 코멘트

## Owner
Backend Eng.

## 후속
부모 PACAA-95에서 CEO+보드 가 Naver Search Advisor 콘솔에서 "확인" 클릭 + sitemap 제출 후 close.
