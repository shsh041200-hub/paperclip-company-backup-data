---
name: "[PACAA-322] POST /api/quote-requests + Resend 이메일 연동"
assignee: "backend-engineer"
---

## 목적

[PACAA-322](/PACAA/issues/PACAA-322) plan v2 Phase 1. Backend API 구현 + Resend 이메일 발송.

## 선행 조건

[PACAA-354](/PACAA/issues/PACAA-354) DB migration 완료 후 시작.

## 작업

### 1. Resend 설치
```bash
npm i resend
```

### 2. API route 구현
`app/api/quote-requests/route.ts`

**Request body:**
- vendorIds: string[] (1–3개, is_hidden=false 실존 확인)
- buyerEmail: string (필수, max 255자)
- buyerCompany?: string
- quantityDesc?: string
- deadlineDate?: string (ISO date)
- requirements?: string (min 10자, max 2000자)
- consentCollection: boolean (true 필수 — §15)
- consentThirdParty: boolean (true 필수 — §17)
- _honey?: string (honeypot — 값 있으면 fake 201, 실제 저장 skip)

**Rate limiting:** ip_hash(SHA-256(x-forwarded-for)) — 10분 내 3회 초과 → 429

**흐름:**
1. honeypot 체크
2. 동의 2개 모두 true 검증 (하나라도 false → 400)
3. vendorIds Supabase 실존·is_hidden 검증
4. DB INSERT (status=pending, consent_collection_at=now(), consent_third_party_at=now())
5. Resend API — vendor당 이메일 1통 (companies.email 사용, 없으면 skip+log)
6. Resend API — buyer 접수 확인 이메일 1통
7. DB UPDATE status=sent

**응답:** 201 {quoteRequestId}, 400, 429, 500

### 3. 환경변수
`RESEND_API_KEY` — .env.local + Vercel 등록 (CEO 액션 대기 중)

## Plan 참조

[PACAA-322 Plan §3-§5](/PACAA/is
