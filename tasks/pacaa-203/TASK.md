---
name: "[hreflang 일괄 수정 → CTO] label-printing + flexible-packaging x-default 누락 + sitemap"
assignee: "cto"
---

## 배경

전체 16개 가이드 hreflang + sitemap 전수 감사 결과 2개 가이드 이슈 발견.

## 수정 사항

### 1. label-printing-guide — x-default 누락

현재: `<link rel="alternate" hrefLang="ko-KR" .../>`
필요: ko-KR + x-default 두 태그 모두 필요

```html
<link rel="alternate" hrefLang="ko-KR" href="https://packlinx.com/guides/label-printing-guide"/>
<link rel="alternate" hrefLang="x-default" href="https://packlinx.com/guides/label-printing-guide"/>
```

### 2. flexible-packaging-guide — x-default 누락 + sitemap 미등재

현재: ko-KR만 있음, sitemap/0에 없음
필요: x-default 태그 추가 + sitemap 등재

## 검증 방법

```bash
# x-default 확인
curl -sL https://packlinx.com/guides/label-printing-guide | grep -i 'x-default'
curl -sL https://packlinx.com/guides/flexible-packaging-guide | grep -i 'x-default'
# sitemap 확인
curl -s https://packlinx.com/sitemap/0 | grep flexible-packaging
```

## 참고

`plastic-container-guide` — ko-KR + x-default 모두 정상 ✅ (동일 패턴 적용)
나머지 14개 가이드는 모두 hreflang + sitemap 완전 정상.
