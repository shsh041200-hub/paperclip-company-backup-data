---
name: "[PACAA-228 child] Disk IO 완화 — sitemap force-dynamic 제거 + /companies/[slug] auth 클라이언트 분리"
assignee: "frontend-engineer"
---

## 배경

PACAA-228 (parent): Supabase 가 `pkging-platform` 의 Disk IO Budget 소진 알림 발송. CEO 진단 결과 sitemap 3개 라우트 + /companies/[slug] 페이지가 모두 `force-dynamic` 으로 매 요청 DB 직격 = IO 폭주 주범 가설. 보드는 Option A (코드 fix만, $0/월) 선택.

## 변경 대상 (3개 파일)

레포: `~/.paperclip/instances/default/projects/d5e183da-c58f-4124-8075-493330dce4c4/f0cad884-57d7-4a3e-b1bb-fa93a4fc0b2c/pkging-platform`

### A. sitemap index 캐시 활성화 (간단)
파일: `src/app/sitemap.xml/route.ts`
- 라인 13 `export const dynamic = 'force-dynamic'` **삭제**
- 라인 14 `export const revalidate = 3600` **유지**
- Cache-Control 헤더는 이미 `public, max-age=3600` 으로 설정돼있음 — 그대로

### B. sitemap shard 캐시 활성화 (간단)
파일: `src/app/sitemap/[id]/route.ts`
- 라인 21 `export const dynamic = 'force-dynamic'` **삭제**
- 라인 22 `export const revalidate = 3600` **유지**

### C. /companies/[slug] auth 클라이언트 분리 (refactor)
파일: `src/app/companies/[slug]/page.tsx`
- 라인 43 `export const dynamic = 'force-dynamic'` 및 라인 41-42 코멘트 **삭제**
- `export const revalidate = 3600` **추가**
- `Promise.all` (라인 103-123) 의 첫 번째 element `isOwner` 계산 (라인 104-113, `supabase.auth.getUser()` + user_profiles 조회) **분리** → 새 클라이언트 컴포넌트 `OwnerControls.tsx` (or 기존 client component 가 있으면 거기에) 가 페이지 mount 후 `/api/compan
