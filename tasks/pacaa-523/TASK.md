---
name: "[FE] PACAA-516 — Footer 「Packlinx 자체 등록 기준 안내」 링크 추가 (LC §4-A P1)"
assignee: "frontend-engineer"
---

## 배경

[PACAA-516](/PACAA/issues/PACAA-516) Phase B2 CMO 위임 sub-task (P1 — 권장). Legal Counsel [PACAA-509](/PACAA/issues/PACAA-509) §4-A Surface: Footer 에 FAQ 링크 노출.

## 구현 스펙

### 링크 카피

`Packlinx 자체 등록 기준 안내`

### 링크 URL

`/faq#what-is-jeongbo-deungrok`

### 적용 위치

- `app/page.tsx` footer nav 링크 목록에 추가
- 기타 공통 footer 가 사용되는 모든 페이지

### 참고 — 현재 footer 링크 목록 (`app/page.tsx` 약 L987~993)

```
키워드 디렉터리 | 패키징 가이드 | 개인정보처리방침 | 이용약관 | 권리침해 신고
```

이 목록에 `자주 묻는 질문` 또는 `Packlinx 자체 등록 기준 안내` 링크를 추가.

## Acceptance

- [ ] Footer 에 링크 정상 노출
- [ ] /faq#what-is-jeongbo-deungrok 이동 확인
- [ ] 모바일 footer 에서도 노출 확인

## 의존

- [PACAA-516](/PACAA/issues/PACAA-516) FAQ 페이지 PR #61 머지 후 링크 유효

parent: PACAA-516
