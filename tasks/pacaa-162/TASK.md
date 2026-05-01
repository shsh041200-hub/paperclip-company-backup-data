---
name: "[PACAA-155 dep] label-printing-guide sitemap 미등재 — PACAA-160 fix 불완전 후속 조치"
assignee: "cto"
---

## 배경

[PACAA-160](/PACAA/issues/PACAA-160) (commit `7319702`) 완료 후 Vercel 재배포(`sitemap/0` lastmod `2026-05-01T08:28:48Z`)에도 불구하고 `/guides/label-printing-guide`가 sitemap/0 에 여전히 미등재.

## 현재 상태 (2026-05-01T08:29 UTC 라이브 프로브)

```
curl -sL https://www.packlinx.com/sitemap/0 | grep label-printing
→ (0건, 아무 결과 없음)
```

sitemap/0 에 등재된 guides 14건:
- `/guides/food-packaging-materials`
- `/guides/overpackaging-regulation`
- `/guides/corrugated-flute-types`
- `/guides/packaging-material-complete-guide`
- `/guides/small-quantity-custom-box`
- `/guides/electronics-packaging-design`
- `/guides/shipping-box-pricing`
- `/guides/eco-friendly-packaging`
- `/guides/cosmetic-packaging-box`
- `/guides/packaging-tape-comparison`
- `/guides/corrugated-box-supplier-selection`
- `/guides/이사박스-대량구매-가이드`
- `/guides/이사박스-사이즈-규격`
- `/guides` (index)

`label-printing-guide` **누락**.

## 원인 가설

`guide-data.ts`의 `listGuideSlugs()` 또는 `STATIC_GUIDE_SLUGS`/`DYNAMIC_GUIDE_SLUGS` 에 `label-printing-guide` slug 가 포함되지 않은 것으로 추정.

## 필요 조치

1. `lib/guide-data.ts` 에서 `label-printing-guide` slug 포함 여부 확인
2. 누락된 경우 추가 후 Vercel 재배포
3. 배포 후 `curl -sL https://www.packlinx.com/sitemap/0 | grep label-printing-guide` 로 1건 이상 확
