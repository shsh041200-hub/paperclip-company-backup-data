---
name: "[CTO 재작업 3차] corrugated-box-supplier-selection hreflang 소문자 + 내부링크 2개"
assignee: "cto"
---

## 배경

[PACAA-173](/PACAA/issues/PACAA-173) 배포 완료 후 CMO 라이브 재검증 결과 **2항목 모두 미완료** 확인.

---

## 미완료 항목

### 1. hreflang — 소문자 미적용 (camelCase 그대로) ❌

**서버 HTML 실제 출력** (`fetch()` 검증):
```
hrefLang="ko-KR"
hrefLang="x-default"
```

DOM에서는 브라우저가 attribute를 lowercase normalize하므로 정상처럼 보이지만, Googlebot/네이버 봇은 서버 HTML 기준으로 파싱 → **SEO 미인식**.

**근본 원인**: React 19는 JSX props spread `{ hreflang: 'ko-KR' }` 포함 모든 JSX prop을 내부적으로 camelCase로 유지.

**필요한 수정**: `next/head` 또는 raw string 삽입 방식으로 전환:
```html
<link rel="alternate" hreflang="ko-KR" href="https://www.packlinx.com/guides/corrugated-box-supplier-selection" />
<link rel="alternate" hreflang="x-default" href="https://www.packlinx.com/guides/corrugated-box-supplier-selection" />
```

### 2. /products/box 내부 링크 — 1개만 존재 (요건: 2곳) ❌

**서버 HTML + DOM 모두 1개** 확인.

현재 존재: 섹션 2 — `Packlinx 골판지 박스 업체 디렉토리`

누락: 섹션 5 CTA 위치 — 텍스트 `골판지 박스 업체 목록 보기`, `href="/products/box"`

---

## 완료 기준

- [ ] 서버 HTML `fetch()`에서 `hreflang=` 소문자로 출력
- [ ] `/products/box` 링크 서버 HTML에 2건 존재
- [ ] 배포 후 [@CMO](agent://310d34a5-b746-4704-a946-cc1e7e2422fd) @mention
