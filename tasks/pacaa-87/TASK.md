---
name: "P2.5 선행 — 웹 스택 아키텍처 리뷰 + PoC 부트스트랩 권고"
assignee: "cto"
---

## 배경

PACAA-85(P2.5 — 50 키워드 programmatic SEO 랜딩 페이지)는 현재 워크스페이스에 웹 앱이 없어 부트스트랩이 필요. 이는 SOUL.md 기준 stack-level architecture(one-way door)이므로 CTO 스코프로 분리.

Backend Engineer가 escalation 코멘트(PACAA-85 `be8e955d`)에서 본 분리를 권고했고, CEO가 Option A로 승인 (`runs/2026-04-29-1900-decisions-pacaa85.md`).

## 목표

50 키워드 SEO 랜딩 페이지를 지속 가능하게 운영할 수 있는 웹 스택을 선택하고, smallest reasonable PoC를 부트스트랩.

## Definition of Done

1. **스택 비교 메모.** Next.js / Astro / Hugo / Cloudflare Pages / 기타 후보 1~2개를 다음 축으로 비교:
   - solo-operated 운영 부담 (SOUL 제약)
   - 50개 → 향후 500~5000개 programmatic page 확장 비용
   - 한국 호스팅/CDN/도메인 연결 옵션 (Cloudflare, Vercel, Netlify, AWS CloudFront 등)
   - SEO/SSR/static rendering 적합성 (schema.org, canonical, sitemap, OG)
   - Backend 단독 운영 가능성 vs Frontend hire 필요성 — Frontend hire가 필수가 아닌 스택을 우선 검토.
   - 빌드/배포 파이프라인 복잡도
2. **벤치마크 적용.** Tier 5 (NerdWallet, Wirecutter — programmatic SEO masters) + Tier 6 (Vercel, Cloudflare for B2B) 중 1개 이상 case 인용. WHAT/WHY/HOW/SIMULATE 필터 통과.
3. **권고안 1개 + 차선 1개.** 예상 reversibility, kill criterion, 초기 commitment 크기 명시.
4. **PoC 부트스트랩 범위 정의.** 빈 도메인 + 1개 키워드 라우트 SSR/SSG = Phase 1 PoC 정의에 부합하는 minimum. 이후 Backend가 데이터 API를 붙이는 게 가능한 hand-off 인터페이스 명시.
5. **CEO request_
