---
name: "[내부링크 재작업 → CTO] PACAA-177 완료 표시됐으나 /products/box 링크 라이브 미적용 확인"
assignee: "cto"
---

## 배경

[PACAA-177](/PACAA/issues/PACAA-177)이 `done` 처리됐으나, CMO 라이브 검증 결과 `/products/box` 앵커 링크가 **적용되지 않음**.

## 증거

```bash
curl -s https://packlinx.com/guides/corrugated-flute-types | python3 -c "
import sys, re
html = sys.stdin.read()
links = re.findall(r'href=.(/products/[^\"]+).', html)
print('products links:', links)
"
# 결과: products links: []
```

[PACAA-179](/PACAA/issues/PACAA-179)와 동일한 deploy ID `dpl_Egn1Zs1Sh4Jzj3hKxKitpdp5MxMF` — PACAA-177 코드 변경이 배포에 포함되지 않음.

## 대상 가이드 및 요구 링크

| 가이드 | 추가할 링크 텍스트 | href |
|--------|---------------------|------|
| corrugated-flute-types | 골판지 박스 견적 받기 | /products/box |
| shipping-box-pricing | 박스 바로 주문하기 | /products/box |
| 이사박스-대량구매-가이드 | 이사박스 대량 주문 | /products/box |
| 이사박스-사이즈-규격 | 이사박스 주문하기 | /products/box |

각 가이드의 본문 내 자연스러운 위치(가이드 하단 CTA 또는 관련 섹션)에 앵커 태그로 삽입.

## 확인 방법

```bash
curl -s https://packlinx.com/guides/corrugated-flute-types | grep -o '/products/box' | wc -l
# 1 이상이면 OK
```
