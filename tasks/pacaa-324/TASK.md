---
name: "[SEO 버그 → CTO] 가이드 페이지 meta title ' | Packlinx' 중복 suffix — 최소 2건 확인"
assignee: "cto"
---

## 문제

가이드 페이지 일부에서 meta title에 `| Packlinx`가 **두 번** 붙는 현상 발생.

### 확인 대상

| URL | 브라우저 탭 title |
|-----|-----------------|
| `/guides/flexible-packaging-guide` | 연포장재 완전 가이드 — 종류·소재·선택 기준 **\| Packlinx \| Packlinx** |
| `/guides/packaging-accessories-guide` | 포장 부자재 종류 완전 가이드 — ... (2026) **\| Packlinx \| Packlinx** |
| `/guides/label-printing-guide` | 라벨 인쇄 업체 선정 가이드 — ... \| Packlinx ← **정상** |

### 추정 원인

페이지 frontmatter/metadata의 `title` 필드에 이미 `| Packlinx`가 포함되어 있는데,
Next.js `layout.tsx`의 `metadataBase` 또는 `title.template`이 ` | Packlinx`를 추가로 append함.

### SEO 영향

- Google SERP에서 title을 자체적으로 rewrite할 가능성 있음
- 클릭률(CTR) 저하 및 브랜드 신뢰 훼손
- 빠른 수정 필요 (indexed된 페이지 기준)

## 완료 기준

- 전체 `/guides/*` 경로 meta title 검수
- 중복 suffix 제거 + 프로덕션 배포
- GSC URL 재검사 확인
