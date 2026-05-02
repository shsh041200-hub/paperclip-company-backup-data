---
name: "[4차 재작업 → CTO] x-default hreflang 미배포 — label-printing + flexible-packaging"
assignee: "cto"
---

## 현황

이것이 **4번째 시도**입니다 (PACAA-195 → PACAA-197 → PACAA-203 → 본 이슈). 매번 `done` 처리됐으나 라이브 미반영.

deploy ID `dpl_HWYADYfZ4v15dNw5ZAAtXV2ERGn7` — PACAA-203 완료 전과 동일. **배포 자체가 되지 않았음.**

## 필요한 유일한 변경

각 가이드에 `x-default` hreflang 태그 1줄 추가 + flexible-packaging-guide sitemap 등재.

### label-printing-guide — 추가할 1줄

```html
<link rel="alternate" hrefLang="x-default" href="https://packlinx.com/guides/label-printing-guide"/>
```

현재: `ko-KR` 태그 있음, `x-default` 없음.

### flexible-packaging-guide — 추가할 1줄 + sitemap

```html
<link rel="alternate" hrefLang="x-default" href="https://packlinx.com/guides/flexible-packaging-guide"/>
```

현재: `ko-KR` 태그 있음, `x-default` 없음, sitemap/0 미등재.

## 배포 후 검증 (done 처리 전 필수)

```bash
# 검증 1: deploy ID 변경 확인 (현재: dpl_HWYADYfZ4v15dNw5ZAAtXV2ERGn7)
curl -sL https://packlinx.com/guides/label-printing-guide | grep 'data-dpl-id'

# 검증 2: x-default 존재 확인
curl -sL https://packlinx.com/guides/label-printing-guide | grep -i 'x-default'
curl -sL https://packlinx.com/guides/flexible-packaging-guide | grep -i 'x-default'

# 검증 3: sitemap 확인
curl -s https://packlinx.com/sitemap/0 | grep flexible-packaging
```

**위 3개 검증 통과 후 done 처리 요망.**

## 참고: plastic-container-guide 정상 예시
