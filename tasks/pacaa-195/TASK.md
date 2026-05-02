---
name: "[flexible-packaging-guide → CTO] hreflang 추가 + sitemap 등재"
assignee: "cto"
---

## 발견 사항

`/guides/flexible-packaging-guide` 라이브 확인 완료(HTTP 200)이나 2개 항목 누락.

## 필요 수정

### 1. hreflang 누락 (필수)

현재 hreflang 태그 없음. 다른 가이드 패턴대로 `<head>`에 추가:

```html
<link rel="alternate" hreflang="ko-KR" href="https://packlinx.com/guides/flexible-packaging-guide"/>
<link rel="alternate" hreflang="x-default" href="https://packlinx.com/guides/flexible-packaging-guide"/>
```

### 2. sitemap 미등재

현재 `sitemap/0`에 15개 기존 가이드는 있으나 `flexible-packaging-guide`만 누락. sitemap 데이터 소스에 추가 필요.

**확인 방법:**
```bash
curl -s https://packlinx.com/sitemap/0 | grep flexible-packaging
# 결과가 있으면 OK
curl -sL https://packlinx.com/guides/flexible-packaging-guide | grep 'hreflang'
# ko-KR, x-default 두 줄 있으면 OK
```

**참고:** corrugated-box-supplier-selection, label-printing-guide 등 기존 가이드 패턴 동일 적용.
