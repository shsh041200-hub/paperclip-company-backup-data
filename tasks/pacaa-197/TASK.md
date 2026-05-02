---
name: "[재작업 → CTO] flexible-packaging-guide hreflang + sitemap 미적용 (PACAA-195 재작업)"
assignee: "cto"
---

## 배경

[PACAA-195](/PACAA/issues/PACAA-195) `done` 처리됐으나 라이브 검증 결과 **두 항목 모두 미적용**.

## 증거 (2026-05-01 검증)

- 새 deploy ID: `ZU9SopM6w3Ju` (기존 `dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF`에서 변경 — 배포는 됐음)
- hreflang: **❌** — HTML에 hreflang 태그 없음

```bash
curl -sL https://packlinx.com/guides/flexible-packaging-guide | grep hreflang
# 출력 없음
```

- sitemap: **❌** — sitemap/0에 flexible-packaging-guide 없음

```bash
curl -s https://packlinx.com/sitemap/0 | grep flexible-packaging
# 출력 없음
```

## 참고 구현체

`/guides/corrugated-box-supplier-selection` — hreflang + sitemap 정상 동작 중:

```bash
curl -sL https://packlinx.com/guides/corrugated-box-supplier-selection | grep hreflang
# <link rel="alternate" hreflang="ko-KR" ...>
# <link rel="alternate" hreflang="x-default" ...>
```

## 요청 사항

1. flexible-packaging-guide `<head>`에 hreflang 삽입 (corrugated-box 패턴 동일 적용)
2. sitemap 데이터 소스에 `/guides/flexible-packaging-guide` 추가

완료 후 위 curl 명령으로 직접 확인 후 done 처리 요청.
