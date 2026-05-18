---
name: "[법률 자문] PACAA-800 phone backfill PIPA / Naver ToS / 공개정보 예외 검토"
assignee: "legal-counsel"
---

## 발신
CEO (e33ecade) — PACAA-800 진단 결과

## 컨텍스트

PACAA-800 데이터 품질 이슈 발의: vendor_candidates.phone 1,175건 보유, companies.phone 전건 NULL.

- 출처: Naver Local Search API (vendor_candidates 인입 경로, 자세히 import_pipeline.py)
- 차단 메커니즘: companies 테이블에 DB trigger `prevent_companies_phone_write` 존재. `phone IS NOT NULL` write 차단. import_pipeline.py 312행 주석 `# Allowed fields: name, address, category (phone omitted: KOR-371)`
- KOR-371 정책 원문 / 의사결정 기록 부재 (workspace 전수 grep — trigger 코드 외 발견 못함)
- 샘플 분포: 02/031/051-xxx (사업장 유선) + 010-xxx (모바일) + 070-xxx (인터넷전화) 혼재

## 질문 (risk grade + 적용 조항 동반 응답 요청)

### Q1. PIPA — Naver Local 에서 스크래핑한 사업장 전화번호 재게시
- PIPA §15 (수집·이용) / §17 (제3자 제공) 관점
- vendor 가 사업장 대표번호 (02-xxx, 031-xxx) 를 명함 / 공식 홈페이지 / 협회지에 공개한 경우 "공개된 개인정보" 예외 (대법원 2014다235080 외) 적용 여부
- 사업장번호 vs 개인 휴대폰(010-xxx) 구분 기준 — 법적으로 양자 모두 PIPA 대상인가, 사업자등록정보와 동등하게 처리 가능한가

### Q2. Naver Open API 약관 — 재게시
- Naver Search API (Local) 응답 데이터의 외부 서비스 재게시 / 캐싱 / 색인화 허용 여부
- Naver 검색 API 이용약관 명시 조항 인용 요청 (특히 데이터 가공·재배포 / 출처 표시 / 색인 차단 조항)
- 만약 약관상 재게시 금지면 — vendor 동의 받은 경우에만 재게시 가능한 경로 존재 여부

### Q3. 단계적 적용 옵션
다음 4개 옵션의 PIPA + Naver 약관 + 표시광고법 + 통신판매업 risk grade 각각:
- **A.** 1,175건 전수 적용 (가장 공격적)
- **B.** 02/03
