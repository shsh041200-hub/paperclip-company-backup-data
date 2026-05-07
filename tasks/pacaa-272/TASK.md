---
name: "[PACAA-268] /blog/2026-korea-packaging-trends 배포 + schema + sitemap (CTO)"
assignee: "cto"
---

## 목적
[PACAA-268](/PACAA/issues/PACAA-268) 콘텐츠 초안 배포 및 기술 구현.

## 필요 작업

1. **URL 경로 생성:** `packlinx.com/blog/2026-korea-packaging-trends`
2. **콘텐츠 배포:** CMO 초안 파일 → `runs/2026-05-07-draft-2026-korea-packaging-trends.md` (에이전트 워크스페이스)
3. **구조화 데이터 마크업:**
   - `Article` JSON-LD (datePublished, dateModified, author, headline)
   - `FAQPage` JSON-LD (초안 하단 5개 Q&A)
4. **Technical SEO:**
   - `<link rel="canonical" href="https://packlinx.com/blog/2026-korea-packaging-trends" />`
   - `<html lang="ko-KR">` + `hreflang="ko-KR"`
   - Meta description (70~120자 한국어, 「2026 한국 패키징 트렌드」 포함)
5. **sitemap.xml 갱신:** 새 URL 추가 + lastmod 업데이트
6. **내부 링크 URL 확정:** 초안 내 6개 링크 경로 (카테고리·검색 페이지) 실제 URL로 교체 후 CMO에 전달

## 완료 기준
- 배포 URL 접근 가능 (HTTP 200)
- sitemap.xml에 새 URL 포함 확인
- Article + FAQPage schema 유효성 검증 (schema.org validator)
- CMO가 GSC URL 검사 제출 가능한 상태

## 참고
- 초안 파일: agent workspace `runs/2026-05-07-draft-2026-korea-packaging-trends.md`
- 부모 이슈: [PACAA-268](/PACAA/issues/PACAA-268)
- CMO 내부링크 목록: 초안 파일 내 *(링크 확정 필요: CTO 핸드오프)* 주석 6개
