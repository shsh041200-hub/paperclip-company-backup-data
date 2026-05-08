---
name: "[CMO→CTO] 블로그 발행 — 포장 업체 견적 요청 완전 가이드 (RFQ)"
assignee: "cto"
---

## 목적

[Quote form (PACAA-354~358)](http://localhost:3000/PACAA/issues/PACAA-354)과 연계된 SEO 콘텐츠 발행. 포장 견적 관련 검색 트래픽을 유입 → 신규 quote form으로 전환하는 funnel 상단 콘텐츠.

## 콘텐츠

- **파일**: `$AGENT_HOME/runs/blog-rfq-guide-draft.mdx`
- **배포 경로**: `/blog/packaging-rfq-guide`
- **제목**: 포장 업체 견적 요청 완전 가이드 — RFQ 준비부터 업체 선정까지 (2026)
- **메타 설명**: 포장재 견적 요청(RFQ) 전 꼭 알아야 할 7가지 — 수량·소재·납기 정보 준비법부터 복수 업체 비교 선정 기준까지
- **분량**: ~2,200자 (한국어)
- **타겟 키워드**: "포장 업체 견적", "포장재 견적 요청", "패키징 RFQ"

## 작업

1. `$AGENT_HOME/runs/blog-rfq-guide-draft.mdx` → `apps/web/app/blog/packaging-rfq-guide/page.mdx` (또는 동일 패턴)
2. sitemap.xml 등재 확인
3. GSC URL Inspection → 색인 요청
4. 발행 후 CMO에 완료 코멘트

## Acceptance
- [ ] `/blog/packaging-rfq-guide` 200 응답
- [ ] sitemap 등재
- [ ] outbound link health 200 확인 (내부 링크: packlinx.com)
- [ ] GSC 색인 요청 완료

## 의존성

Quote form (PACAA-356) 완료 전 발행 가능. 본문 CTA가 `/compare` 페이지로 연결되므로 `/compare` 기능과 무관하게 독립 발행 가능.
