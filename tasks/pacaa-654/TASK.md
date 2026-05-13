---
name: "Company export API: 500 when include.issues=true"
assignee: "cto"
project: "packlinx-website"
---

## 증상

`POST /api/companies/{companyId}/export` 가 `include.issues=true` 일 때 항상 `HTTP 500 {"error":"Internal server error"}` 반환. 어제(2026-05-12 23:00 KST)까지는 정상 동작 (2.1MB 스냅샷 push 완료).

## 재현 (2026-05-13 14:00 UTC, 7회 연속 500)

```
POST $PAPERCLIP_API_URL/api/companies/d5e183da-c58f-4124-8075-493330dce4c4/export
body: {"include":{"company":true,"agents":true,"skills":true,"projects":true,"issues":true}}
→ HTTP 500, body 33B {"error":"Internal server error"}
```

## 격리

`issues` 플래그만 빼면 200. 7회 모두 issues 포함 시만 500.

| include | result |
|---|---|
| company | 200 (497970B) |
| +agents | 200 |
| +skills | 200 |
| +projects | 200 (499057B) |
| +issues | **500** |

별도로 `GET /api/companies/{id}/issues?limit=1` 는 200 정상 — issues 도메인 자체는 살아 있음. export 직렬화 단계에서만 깨짐. 어제 → 오늘 사이에 추가된 issue 중 직렬화 에러를 트리거하는 데이터(예: 오버사이즈 필드, 새 스키마 미마이그레이션 컬럼)가 의심됨.

## 영향

PACAA-653 (Daily Company Packages backup) 가 오늘 23:00 KST fire 에서 멈춤. 부분 백업(issues 제외)을 푸시하면 백업 repo 히스토리에서 issues 디렉토리가 삭제 커밋되어 더 큰 손상. 오늘은 푸시 보류.

## 요청

1. export 엔드포인트 issues 직렬화 경로 디버그 (서버 로그 확인 — 33B 응답이라 client-side 단서 없음).
2. 핫픽스 후 PACAA-653 보드/CEO 에 알리고, 오늘자 백업을 catch-up 으로 한 번 더 fire (또는 내일 정기 fire 로 cover).
3. 회귀 방지: export 엔드포인트에 issue
