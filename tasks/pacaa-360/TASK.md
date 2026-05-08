---
name: "[FIX] dev 서버 Internal Server Error 해소 — 중복 동적 라우트 [id] 디렉터리 삭제"
assignee: "cto"
---

## 배경
PACAA-359 진단 결과: `npm run dev` 가 동적 라우트 segment param 이름 충돌 2건으로 `unhandledRejection` 발생, 페이지 접근 시 Internal Server Error.

## 근본 원인
오늘 09:52 에 추가된 두 디렉터리가 같은 path level 의 기존 segment 와 다른 param 이름을 써서 Next.js App Router 가 라우트 트리를 빌드 못함.

## Scope (보드 OK 받음 — A안)
다음 두 디렉터리 삭제:
1. `app/sitemap/[id]/` — `app/sitemap/[__metadata_id__]/route.ts` 와 글자 한 자도 다르지 않은 복사본 (둘 다 242줄). 출력 동일.
2. `app/api/companies/[id]/` — 안의 `similar-optout/route.ts` 가 `app/api/companies/[slug]/similar-optout/route.ts` 와 중복 가능성. 삭제 전 두 파일 diff 먼저 확인, 만약 다르면 [slug] 쪽으로 통합.

## 출력 보존 보장 (보드 우려)
구글/네이버 제출 sitemap URL (/sitemap.xml, /sitemap/0, /sitemap/1 등) 은 다음 두 파일이 응답 — 둘 다 보존:
- app/sitemap.ts (78줄, /sitemap.xml)
- app/sitemap/[__metadata_id__]/route.ts (242줄, sharded)

## Acceptance
1. app/sitemap/[id]/ 디렉터리 삭제 후 dev 서버 재시작 → unhandledRejection 사라짐
2. app/api/companies/[id]/ diff 확인 후 처리 (삭제 또는 통합)
3. 로컬 검증:
   - curl http://localhost:3000/sitemap.xml → 200, XML 응답
   - curl http://localhost:3000/sitemap/0 → 200, sharded XML
   - 메인 페이지 /, /companies/<slug>, /guides/<slug> 라이브 200 확인
4. production 배포 후 https://www.packlinx.com/sitemap.xml + /sitemap/0 200 재확인 (구글/네이버 인덱스 보존 검증)

## Out of scope (별도 처리)
