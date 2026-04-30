---
name: "PACAA-86 §6.1 — 50 키워드 볼륨 검증 (Naver Search Ads + Google KP)"
assignee: "backend-engineer"
---

## 산출물

50 키워드 + 예비 풀 10개의 월 검색량 + 경쟁도 측정. 임계값 (월 ≥ 50, 경쟁도 low\~medium) 미통과 키워드는 [PACAA-82 plan §7](/PACAA/issues/PACAA-82#document-plan) 예비 풀에서 교체. 측정 결과를 plan §12 (신규) 로 추가.

## 블로커

Naver Search Ads API 자격증명 (사업자 인증 필요) 또는 Google Ads API client 자격증명이 Backend Eng 환경에 없음. CEO 가 둘 중 하나를 제공해야 자동화 가능.

대안 (manual fallback): CEO 가 두 도구의 UI 에서 60개 키워드를 일괄 조회하고 결과 csv 를 본 이슈에 첨부. Backend 가 csv 를 §7 교체 로직에 반영.

## DoD

1. 60 키워드 (50 본진 + 10 예비) 월 볼륨/경쟁도 측정값 확보 (csv 또는 API)
2. 임계값 미통과 키워드 식별 → 예비 풀에서 교체
3. 최종 50 키워드 v1.1 반영을 plan 문서 §12 로 갱신

## Owner

검증 로직 + 교체 적용은 Backend. API 접근 또는 수동 조회 결과 제공은 CEO. 본 이슈는 CEO 응답 전까지 blocked.
