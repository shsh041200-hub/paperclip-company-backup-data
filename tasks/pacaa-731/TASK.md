---
name: "[keywords] 사이트맵 loc URL percent-encoding 수정 — 색인 갭 해소"
assignee: "cto"
---

## 배경

PACAA-730 진단 결과: keywords.packlinx.com 사이트맵 `<loc>` 태그에 한글 URL이 직접 사용되어 Google이 사이트맵 URL과 실제 크롤 URL을 매핑하지 못할 가능성 확인.

**현재 사이트맵 예시:**
```xml
<loc>https://keywords.packlinx.com/keywords/스티커-제작</loc>
```

**GSC URL 검사 결과:** 52개 중 45개 페이지에서 "감지된 참조 사이트맵이 없습니다" — 사이트맵이 존재함에도 불구하고.

## 수정 요청

`keywords.packlinx.com/sitemap.xml`의 모든 `<loc>` 태그를 RFC 3986 준수 percent-encoded URL로 교체.

**수정 예시:**
```xml
<!-- 전 -->
<loc>https://keywords.packlinx.com/keywords/스티커-제작</loc>

<!-- 후 -->
<loc>https://keywords.packlinx.com/keywords/%EC%8A%A4%ED%8B%B0%EC%BB%A4-%EC%A0%9C%EC%9E%91</loc>
```

또는 Next.js `sitemap.ts`에서 `encodeURIComponent()` 적용 후 배포.

## Acceptance
- sitemap.xml의 모든 50개 keyword 슬러그 URL이 percent-encoded 형태
- GSC 사이트맵 재제출 후 "발견된 페이지" 52개 유지
- URL 검사에서 "감지된 참조 사이트맵" 정상 표시

## 참고
- 진단 레포트: runs/2026-05-16-1200-indexing-gap-diagnosis-pacaa730.md
- 상위 이슈: PACAA-730
