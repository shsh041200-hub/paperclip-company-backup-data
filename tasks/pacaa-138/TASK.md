---
name: "/api/admin/dashboard 응답 shape 와 page 기대 shape 불일치 — 데이터 항상 빈 fallback"
assignee: "backend-engineer"
---

## 배경
PACAA-136 (대시보드 라이브 상태 패널) 작업 중 발견. 현재 `/admin/dashboard` 페이지가 데이터를 항상 빈 fallback 으로만 보여주고 있음.

## 문제
`/api/admin/dashboard?month=YYYY-MM` 의 응답 shape 와 `src/app/admin/dashboard/page.tsx` 가 기대하는 shape 가 불일치:

**API 응답 (route.ts):**
```json
{
  "period": { "from": "...", "to": "..." },
  "monthlyLeads": { "YYYY-MM": number, ... },
  "leadsByCompany": [{ "companyId", "name", "count" }, ...],
  "leadsByCategory": { "category": number, ... },
  "conversionFunnel": { ... }
}
```

**Page 가 기대하는 shape (page.tsx 의 dashboardData 타입):**
```json
{
  "monthly_leads": number,
  "daily_leads": [{ "date", "count" }, ...],
  "category_distribution": [{ "category", "count" }, ...],
  "top_companies": [{ "name", "slug", "lead_count" }, ...]
}
```

키 이름과 구조 둘 다 다름. fetch 후 page 가 `dashboardData.monthly_leads` 를 읽으면 `undefined` → 화면에 0 표시됨. 또한 page 가 보내는 `?month=YYYY-MM` 쿼리 파라미터도 API 에서 무시됨 (API 는 `from`/`to` 만 인식).

## 영향
- 관리자 대시보드 모든 KPI/차트/표가 빈 상태로 보임
- 신규 추가된 LiveStatusPanel 도 fallback 빈 데이터로 동작 → "아직 없어요" 류 문장만 노출
- 보드가 실제 회사 상황을 대시보드로 파악 불가

## 해결 방향 (제안)
1. API 응답을 page 가 기대하는 shape 로 맞추기 (가장 깔끔):
   - `monthly_leads`: 선택된 월의 합계
   - `daily_leads`: 선택된 월의 일자별 카운트 (지금은 월 단위로만 집계)
   - `cat
