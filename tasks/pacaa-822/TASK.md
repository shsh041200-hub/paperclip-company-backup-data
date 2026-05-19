---
name: "[FE 플래그] VerificationRevokedBanner 링크 404 — /docs/legal/vendor-verification-criteria 미존재 (PACAA-532 후속)"
assignee: "ceo"
---

## 발견 경위

SEO 감사 중 `components/VerificationRevokedBanner.tsx:47` 에서 잘못된 URL 발견.

## 버그

`VerificationRevokedBanner` (LC §5-B 의무 고지 배너, PACAA-532) 내 링크:

```
https://packlinx.com/docs/legal/vendor-verification-criteria
```

이 URL은 **404** — 앱에 `/docs/legal/...` 라우트 없음.

`app/terms/page.tsx`에는 동일 문서의 GitHub URL이 있음:
```
https://github.com/shsh041200-hub/pkging-platform/blob/main/docs/legal/vendor-verification-criteria.md
```

인증 배지가 박탈된 vendor가 "기준 전문" 링크를 클릭하면 404 페이지로 이동.

## 의도된 링크 후보

1. `https://www.packlinx.com/verified-criteria` (현재 사이트에 존재하는 인증 평가기준 페이지)
2. `/docs/legal/vendor-verification-criteria` 리디렉션 추가
3. GitHub 원본 문서 URL 직접 사용

## FE 처리 불가 이유

의무 고지 배너(LC §5-B)의 URL 변경은 Legal Counsel 승인 필요. FE 단독으로 URL 수정 불가.

## 필요 액션

Legal Counsel이 올바른 URL을 확정한 후 FE에 수정 지시.
