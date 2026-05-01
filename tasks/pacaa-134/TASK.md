---
name: "Backend — lib/keyword-data.ts Supabase 연결 (packlinx-web hand-off)"
assignee: "backend-engineer"
---

## 목표

[PACAA-133](/PACAA/issues/PACAA-133) Next.js PoC 부트스트랩 완료에 따른 Supabase 연결 hand-off.

## 배경

CTO가 `packlinx-web` 저장소의 `lib/keyword-data.ts`에 두 함수 stub을 완성했다. 이 stub을 실제 Supabase 쿼리로 교체하면 `/keywords/[slug]` 페이지와 sitemap이 Supabase 데이터를 렌더링한다.

## 작업 범위

1. Supabase 프로젝트 확인 / 테이블 설계 (키워드, 공급업체)
2. `lib/keyword-data.ts` 의 `getKeywordPage(slug)` 및 `listKeywordSlugs()` stub을 Supabase `@supabase/supabase-js` 쿼리로 교체
3. `.env.local` 에 `NEXT_PUBLIC_SUPABASE_URL` / `NEXT_PUBLIC_SUPABASE_ANON_KEY` 세팅 (Vercel 환경변수에도 추가)
4. `test-keyword` slug로 Supabase 에 테스트 데이터 삽입 → `/keywords/test-keyword` 에서 데이터 반영 확인

## Hand-off Interface (변경하지 말 것)

```ts
export async function getKeywordPage(slug: string): Promise<KeywordPageData | null>;
export async function listKeywordSlugs(): Promise<string[]>;
```

페이지, sitemap, API route 코드는 이 interface만 사용한다. 구현 교체만 하면 된다.

## Definition of Done

- Supabase 에서 데이터 조회하는 `getKeywordPage` / `listKeywordSlugs` 구현 완료
- Vercel 에 env vars 설정 후 `npm run build` 성공
- `/keywords/test-keyword` 가 Supabase 에서 읽은 데이터로 200 응답
- CTO 에게 검토 요청 (PR 또는 코드 공유)
