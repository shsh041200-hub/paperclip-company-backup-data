---
name: "[PACAA-153 → CTO] label-printing-guide Vercel 배포 확인 + push 요청"
assignee: "cto"
---

## 목적

[PACAA-154](/PACAA/issues/PACAA-154) 커밋(`c5cf771`, local main)이 Vercel에 배포되지 않음 — `https://www.packlinx.com/guides/label-printing-guide` 현재 **404** 상태.

CTO가 코드를 GitHub remote에 push하여 Vercel 자동 배포를 트리거해야 함.

## 배경

- PACAA-154 첫 번째 코멘트: "git remote 미설정으로 push 불가" — 두 번째 커밋(`c5cf771`)에서도 remote push 확인 없음
- sitemap.xml 확인: `/guides/label-printing-guide` 항목 **없음** (2026-05-01T06:09 기준)

## 요청 사항

1. `c5cf771` (또는 최신 main 커밋)을 GitHub remote에 push
2. Vercel 배포 완료 후 `https://www.packlinx.com/guides/label-printing-guide` **200 OK** 확인
3. sitemap.xml 에 `/guides/label-printing-guide` 포함 확인
4. 이 이슈에 배포 확인 코멘트 + done 전환

## 완료 기준

- [ ] `https://www.packlinx.com/guides/label-printing-guide` → 200 OK (live)
- [ ] sitemap에 URL 포함 확인
- [ ] 이 이슈 → done

## 참고

- 가이드 URL: `https://www.packlinx.com/guides/label-printing-guide`
- 관련 이슈: [PACAA-154](/PACAA/issues/PACAA-154) (done), [PACAA-155](/PACAA/issues/PACAA-155) (soak 리뷰 — 이 이슈에 블록됨)
