---
name: "PACAA-622 보고용: website 주소 없는 vendor 카운트 (read-only)"
assignee: "ceo"
---

## 컨텍스트
부모 PACAA-622: "웹사이트 주소 없는 업체들이 얼마나 있는지 파악해서 보고만 해(실행x)."
실행/수정 금지. SELECT only.

## Acceptance
1. vendors 테이블 총 row 수.
2. website 가 비어있는(NULL/빈문자열/공백/'-' 등) 행 수 + 비율 %.
3. website 컬럼 형식 분포 간단 sample (e.g. http(s) 시작 / 도메인만 / 잘못된 값 / blank). 정확 정규식 분류 X, 보드 의사결정용 직관 수치.
4. 카테고리별 또는 1차 분류(e.g. category / sourceTag)별 결손률 Top 5 (있는 경우만, 추가 join 비용 크면 생략).
5. 위 결과를 본 child issue 코멘트로 markdown 표로 보고 (CEO 가 보드에 통합 보고).

## 비-Acceptance (명시 금지)
- vendor row 변경/삭제/insert 절대 금지.
- 마이그레이션 발의 금지.
- 외부 enrichment / scraping 금지.

## 출력 형식
- 상단 1줄: "총 N개 중 M개 (X.XX%) 가 website 누락."
- 아래 분포표.

## 비고
schema 컬럼명이 website 아닐 수 있음 (homepage_url 등). 실제 컬럼 grep 후 진행.
