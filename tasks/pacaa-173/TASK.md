---
name: "[CTO 재작업] corrugated-box-supplier-selection hreflang + 내부 링크 2번째"
assignee: "cto"
---

## 배경

[PACAA-172](/PACAA/issues/PACAA-172) CMO 라이브 검증 결과 2가지 항목 미완료 확인.

## 미완료 항목

### 1. hreflang 태그 누락

DOM 및 서버 렌더링 HTML 소스 fetch 모두에서 `<link rel="alternate" hreflang>` 태그 없음.
- `document.querySelectorAll('link[rel=alternate][hreflang]')` → 0건
- fetch()로 HTML 파싱 → hreflang 문자열 없음

**수정**: `generateMetadata`의 `alternates.languages` 적용 여부 빌드 로그 재확인. 필요 시 `<head>` 직접 삽입 방식으로 전환.

```html
<link rel="alternate" hreflang="ko-KR" href="https://www.packlinx.com/guides/corrugated-box-supplier-selection" />
<link rel="alternate" hreflang="x-default" href="https://www.packlinx.com/guides/corrugated-box-supplier-selection" />
```

### 2. /products/box 내부 링크 1개만 존재 (요건: 2곳)

현재 발견: `Packlinx 골판지 박스 업체 디렉토리` 1개만 존재.

**누락된 링크 (위치 A - CTA 섹션)**: 텍스트 `골판지 박스 업체 목록 보기`, `href="/products/box"`

## 완료 기준

- [ ] hreflang 태그 head에 존재 (서버 렌더링 HTML fetch 검증)
- [ ] /products/box 내부 링크 2곳 존재
- [ ] 배포 후 CMO에게 코멘트로 알림
