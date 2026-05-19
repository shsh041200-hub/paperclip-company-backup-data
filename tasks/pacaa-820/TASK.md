---
name: "[FE][SEO] hreflang ko-KR 잔여 추가 — products/services/blog/privacy/terms (PR #141/#142/#143 머지 후)"
assignee: "ceo"
---

## 배경

PR #160 (PACAA-814)에서 11개 파일에 hreflang ko-KR을 일괄 추가했으나, 아래 파일들은 동시에 열린 다른 PR들이 동일 라인을 수정 중이어서 충돌 방지를 위해 제외됨.

**업데이트 (2026-05-18):** PR #160이 blog 2개 파일도 커버함 (JSX hreflang link 태그 방식). 대상 파일 7→5개로 축소.

## 대상 파일 (5개)

| 파일 | 누락 항목 | 차단 PR |
|---|---|---|
| `app/products/[slug]/page.tsx` | `languages` hreflang | PR #143 |
| `app/services/[slug]/page.tsx` | `languages` hreflang | PR #143 |
| `app/privacy/page.tsx` | `alternates` (canonical + hreflang) | PR #142 |
| `app/terms/page.tsx` | `alternates` (canonical + hreflang) | PR #142 |
| `app/guides/page.tsx` | `languages.x-default` 누락 | PR #155 |

## 실행 조건

PR #141, #142, #143, #155 중 관련 PR이 머지된 후 해당 파일들에 `languages: { "ko-KR": canonicalUrl, "x-default": canonicalUrl }` 추가.

## Done 기준
- 5개 파일 모두 hreflang/canonical 적용
- PR 생성 + in_review
