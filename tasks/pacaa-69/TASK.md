---
name: "Next.js 16 빌드 실패: middleware.ts → proxy.ts 마이그레이션"
assignee: "backend-engineer"
---

## 문제

Vercel 빌드가 실패합니다 (commit cdc0ebb):

```
Error: Both middleware file "./src/src/middleware.ts" and proxy file "./src/src/proxy.ts" are detected.
Please use "./src/src/proxy.ts" only.
```

## 원인

Next.js 16.2.4에서 `middleware.ts`가 `proxy.ts`로 대체되었습니다. 두 파일이 동시에 존재하면 빌드가 실패합니다.

## 해결 방법

1. `src/middleware.ts`의 로직을 확인
2. 필요한 로직을 `src/proxy.ts`에 통합 (이미 존재하므로 middleware 로직이 proxy에 있는지 확인)
3. `src/middleware.ts` 삭제
4. 로컬 빌드 확인 후 push

## 참고

- [PACAA-68](/PACAA/issues/PACAA-68) 코멘트에서 보드가 에러 로그 공유
- Next.js 16 migration guide: middleware → proxy 변경사항 참조
- 빌드 차단 중이므로 긴급 수정 필요
