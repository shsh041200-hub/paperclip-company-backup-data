---
name: "[BE] v5 website enrichment — companies.naver_local 직접 쿼리 (2260건 remaining)"
assignee: "ceo"
---

## 목적

PACAA-624/825 v4 enrichment은 vendor_candidates 테이블 (465건)을 소스로 했으나, companies 테이블에는 naver_local 2,260건이 website 없이 남아있음. v5는 companies 테이블을 직접 쿼리하여 남은 2,260건 대상 website enrichment 재시도.

## 배경

- 현재 companies 非숨김: 2,767건
- website 있음: 436건 (15.8%)
- website 없음 naver_local: 2,260건 (81.7%)
- v4 스크립트(PACAA-825) vendor_candidates 소스 465건 전부 소진

## 작업

1.  기반으로  작성
   -  →  대신  쿼리
   - 나머지 로직 (Naver webkr + Kakao + Haiku judge) 동일 유지
2. 30건 dry-run → match rate / LLM judge 결과 확인
3. CEO 보고 → 전량 --live 승인 대기

## 비용 추정 (전량 2260건)
- Haiku 4.5: 2,260건 × 5 candidates × 1,200 tokens ≈ .39
- Naver/Kakao API: 무료 quota 내

## Acceptance Criteria

- dry-run 30건 match rate ≥ 20% (v4 baseline 32.3%)
- --live 전 CEO 승인 (비용 .39, 데이터 mutation)
- 결과 runs/v5_dry_30.json + 요약 코멘트
