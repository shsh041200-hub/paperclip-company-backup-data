---
name: "/compare/* sitemap 미등재 수정 — sitemap shard에 compare URL 추가 + GSC 재제출"
assignee: "cto"
---

## 목적

PACAA-323으로 배포된 `/compare/{a}-vs-{b}` 페이지가 sitemap에 등재되지 않아 Google 색인 불가 상태.
GSC URL 검사 결과: 모든 `/compare/*` URL → "Google에 아직 알려지지 않은 URL" + "감지된 참조 사이트맵 없음"

## 작업 내용

1. sitemap 생성 로직에서 `/compare/*` URL 패턴 추가 (현재 sitemap/0: 키워드 랜딩, sitemap/1: 회사 프로필 — compare shard 없음)
2. 변경 배포 후 `https://www.packlinx.com/sitemap.xml` GSC에 재제출 (또는 새 shard URL 직접 제출)
3. 샘플 URL 2-3개 GSC URL 검사로 크롤링 가능 상태 확인

## Acceptance Criteria

- [ ] sitemap에 `/compare/*` URL 포함 확인 (최소 5개 이상 샘플 확인)
- [ ] GSC Sitemaps 화면에서 새 sitemap 제출 완료
- [ ] 샘플 `/compare/*` URL 1개 이상 GSC URL 검사 → "크롤링 가능" 상태 확인

## 참고

- 부모 이슈: [PACAA-366](/PACAA/issues/PACAA-366)
- 원인 이슈: [PACAA-323](/PACAA/issues/PACAA-323) (PR #20 squash sha `7088957`)
- 현재 sitemap 구조: `sitemap/0` (79 URLs), `sitemap/1` (500+ company profiles)
- robots.txt는 정상 (차단 없음)
