---
name: "middleware.ts → proxy.ts 마이그레이션 (Next.js 16 deprecation)"
assignee: "ceo"
project: "packlinx-website"
---

## 배경

Next.js 16에서 `middleware.ts` 컨벤션이 deprecated. 매 `next dev` 시작 시 경고:

> The "middleware" file convention is deprecated. Please use "proxy" instead.

동작에는 영향 없으나 향후 메이저 릴리즈에서 에러로 승격될 가능성. 5분짜리 기계적 마이그레이션.

## 현재 파일

`src/middleware.ts` — 18줄, KOR-560 봇 차단 (Meta/OpenAI/Google 크롤러).

## 작업

1. `src/middleware.ts` → `src/proxy.ts` 파일명 변경 (`git mv`)
2. `export async function middleware` → `export async function proxy`
3. `export const config` 그대로 유지 (matcher 동일)
4. `next dev` 재기동하여 deprecation 경고 사라지는지 확인
5. `/`, `/opt-out` 응답 200 회귀 테스트
6. 봇 차단 동작 확인 (curl with `-H 'User-Agent: GPTBot'` → 403)

## 출처

[PACAA-1](/PACAA/issues/PACAA-1) 프로젝트 확인 중 발견. 옵션 B(별도 티켓 분리) 결정.

## 수용 기준

- [ ] `next dev` 시작 시 middleware deprecation 경고 없음
- [ ] 홈페이지/검색 정상 응답
- [ ] 봇 차단 정규식 그대로 동작 (GPTBot/ChatGPT-User/GoogleOther/Meta-* 403 반환)
- [ ] 커밋 메시지에 `Co-Authored-By: Paperclip <noreply@paperclip.ing>` 포함
