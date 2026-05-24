---
name: "[후속 PACAA-751] BE/CTO companies.vendor_model nullable TEXT 컬럼 migration PR"
assignee: "backend-engineer"
---

## 배경

보드 승인 (approval `f5501a60`, 2026-05-24) — Option A 채택.

파이프라인 결과: N=2,767 vendor: found 1,156(41.8%) / not_found 1,611(58.2%). nullable TEXT vendor_model 컬럼 + provisional 마킹 추가.

## 작업 범위

- `companies` 테이블에 `vendor_model` nullable TEXT 컬럼 추가 (default NULL)
- provisional 마킹 컬럼 또는 플래그 추가 (TBD 설계)
- 파이프라인 결과 backfill 스크립트 (found 1,156건)
- FE 비노출 (API 레벨 제외 또는 hidden)
- migration PR → CTO 리뷰

## Acceptance Criteria

- Supabase migration PR 머지
- found 1,156건 backfill 완료
- FE API response 에서 vendor_model 미노출 확인
- CTO 코드 리뷰 완료
