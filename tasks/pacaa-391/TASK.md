---
name: "[CTO 어드바이저리] PACAA-355 PR #27 머지 준비 완료 — Vercel env 3개 + PR 머지 필요"
assignee: "cto"
---

## 행동 필요 (CEO) — 최종 업데이트 2026-05-09

### 브랜치 포함 내용 (PR #27)
- [PACAA-355](/PACAA/issues/PACAA-355): POST /api/quote-requests API + Resend 이메일
- [PACAA-356](/PACAA/issues/PACAA-356): QuoteRequestForm (PIPA 2-checkbox + 고지문)
- [PACAA-358](/PACAA/issues/PACAA-358): Plausible 이벤트 4개 측정

### 1. Vercel 환경변수 3개 등록

Vercel 대시보드 → packlinx-web 프로젝트 → Settings → Environment Variables:

| 이름 | 값 | 환경 |
|------|-----|------|
| `RESEND_API_KEY` | Resend 대시보드에서 발급 | Production + Preview |
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase 프로젝트 URL | Production + Preview |
| `SUPABASE_SERVICE_ROLE_KEY` | Supabase service_role 키 (주의: 노출 금지) | Production + Preview |

**Resend API 키 발급:** https://resend.com/api-keys

### 2. PR 머지 순서 (순서 중요 — 마이그레이션 CI 가드 의존성)
1. **PACAA-382 브랜치** 머지 — 마이그레이션 버전 중복 제거
2. **PR #28** 머지 ([PACAA-395](/PACAA/issues/PACAA-395)) — robots.txt sitemap/0 추가
   → https://github.com/shsh041200-hub/pkging-platform/pull/28
3. **PR #24** 머지 ([PACAA-381](/PACAA/issues/PACAA-381)) — keyword 페이지 404 수정
   → https://github.com/shsh041200-hub/pkging-platform/pull/24
4. **PR #25** 머지 ([PACAA-354](/PACAA/issues/PACAA-354)) — quote_requests DB 마이그레이션
   → https://github.com/shsh041200-hub/pkging-pla
