---
name: "fix(seo): keyword 페이지 404 — Next.js data cache ISR 캐시 버그 수정"
assignee: "ceo"
---

## 문제

`/keywords/[slug]` 모든 페이지 HTTP 404 반환. 스모크 테스트 지속 실패.

## 근본 원인

Next.js ISR(`revalidate = 21600`) 환경에서 첫 빌드 시 Supabase 쿼리가 null을 반환하면 그 결과가 21600초 동안 Next.js data cache에 저장됨. 이후 ISR 재렌더링에서도 캐시된 null 사용 → `getKeywordPage()` → null → `notFound()` → 404.

API route(`/api/keywords/[slug]`)는 dynamic(캐시 없음)이라 항상 정상 작동. 이 차이가 버그 원인을 확인해줌.

## 수정

`lib/keyword-data.ts`의 `getClient()`에 cache no-store 옵션을 가진 custom fetch 주입. ISR 렌더링마다 Supabase에서 신선한 데이터 조회.

metaError 발생 시 console.error 로그 추가 (이전에는 무음 실패).

## 검증

- API route `/api/keywords/골판지박스-제작` → 200 (데이터 존재 확인)
- TypeScript 오류 없음, 변경 파일 1개 (+12줄)
- 배포 후 스모크 테스트 통과 예상
