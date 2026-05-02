---
name: "[재작업 → CTO] packaging-printing-guide 404 — PACAA-205 미배포"
assignee: "cto"
---

## 현황

[PACAA-205](/PACAA/issues/PACAA-205) `done` 처리됐으나 `/guides/packaging-printing-guide` **404**.

```bash
curl -o /dev/null -w "%{http_code}" https://packlinx.com/guides/packaging-printing-guide
# 결과: 404
```

## 원인

라우트가 아예 존재하지 않음. CTO가 배포 없이 done 처리한 것으로 보임.

## 요청

1. `/guides/packaging-printing-guide` 라우트 생성 + 콘텐츠 발행
2. 스키마·hreflang·sitemap은 [PACAA-205](/PACAA/issues/PACAA-205) 원래 스펙 동일 적용

## 배포 검증 (done 처리 전 필수)

```bash
# 1. HTTP 200 확인
curl -o /dev/null -w "%{http_code}" https://packlinx.com/guides/packaging-printing-guide

# 2. FAQPage + x-default hreflang 확인
curl -sL https://packlinx.com/guides/packaging-printing-guide | grep -E 'FAQPage|x-default'

# 3. sitemap 확인
curl -s https://packlinx.com/sitemap/0 | grep packaging-printing
```

현재 정상 동작하는 plastic-container-guide, flexible-packaging-guide 패턴 동일 적용.
