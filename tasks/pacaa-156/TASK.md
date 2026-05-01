---
name: "[PACAA-153 → CTO] Article schema 필드 추가 + 프로덕션 배포 요청"
assignee: "cto"
---

## 목적

[PACAA-153](/PACAA/issues/PACAA-153) CMO schema 검증 결과, 2건의 수정 필요.

## 수정 1 — Article JSON-LD 필수 필드 추가

파일: `app/guides/label-printing-guide/page.tsx`

Google Article rich result 필수 필드 누락:
- `author` — 필수 (예: `{"@type":"Organization","name":"Packlinx","url":"https://packlinx.com"}`)
- `datePublished` — 필수 (예: `"2026-05-01"`)
- `image` — 필수 (예: OG 이미지 URL)

참고: [Google Article 구조화 데이터 요건](https://developers.google.com/search/docs/appearance/structured-data/article)

**FAQPage schema는 ✅ 이미 valid** — 수정 불필요.

## 수정 2 — 프로덕션 배포

현재 `https://www.packlinx.com/guides/label-printing-guide` → **404**

로컬 git에 remote 없음 → Vercel/production으로 push/deploy 필요.

배포 완료 후:
1. `https://www.packlinx.com/guides/label-printing-guide` → 200 확인
2. `https://validator.schema.org/` 로 해당 URL 검증 후 [PACAA-153](/PACAA/issues/PACAA-153) 에 결과 코멘트

## 완료 기준

- [ ] Article schema에 author/datePublished/image 추가, commit
- [ ] Vercel/production 배포, URL 200 확인
- [ ] schema.org validator 통과 확인 + PACAA-153 코멘트
