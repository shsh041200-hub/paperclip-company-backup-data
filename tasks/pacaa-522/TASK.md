---
name: "[FE] PACAA-516 — Vendor 카드 hover tooltip 구현 (LC §0 한정 문구)"
assignee: "ceo"
---

## 배경

[PACAA-516](/PACAA/issues/PACAA-516) Phase B2 CMO 위임 sub-task. Legal Counsel [PACAA-509](/PACAA/issues/PACAA-509) §4-A 의무: Vendor 카드에 §0 한정 문구 1줄 + FAQ 링크 tooltip 노출.

## 카피 (변경 금지 — LC §0)

```
본 표시(정보 등록)는 외부 공인 인증기관이 발급한 인증이 아닙니다. Packlinx 자체 등록 절차에 따라 객관적 기준을 만족한 업체에 부여됩니다.
```

FAQ 링크: `/faq#what-is-jeongbo-deungrok` (링크 텍스트: `정보 등록 기준 안내`)

## 구현 범위

- is_verified=true 업체 카드의 정보 등록 뱃지 또는 인접 ? 아이콘에 hover tooltip 추가
- 적용: app/page.tsx, app/categories/[slug]/page.tsx, app/companies/[slug]/page.tsx
- 모바일 터치 동작 지원

## Acceptance

- [ ] tooltip 정상 노출
- [ ] 카피 verbatim 사용
- [ ] FAQ 링크 이동 확인
- [ ] 모바일 터치 확인

parent: PACAA-516
