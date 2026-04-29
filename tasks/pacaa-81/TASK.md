---
name: "P2.4 — Naver Search Advisor + Google Search Console 연결"
assignee: "backend-engineer"
---

## 목표
양 엔진(Naver Search Advisor, Google Search Console)에 packlinx 도메인을 등록하고 sitemap 제출까지 완료하여 매주 indexing/impression 데이터를 수신할 수 있는 상태로 만든다.

## Definition of Done
1. Google Search Console — 도메인 verification 완료, sitemap.xml 제출, coverage 리포트 첫 수신 확인.
2. Naver Search Advisor — 사이트 등록 완료, sitemap 제출, RSS/robots 검증, 첫 노출 데이터 수신 확인.
3. 양 엔진 모두 매주 자동 리포트 수신 가능 상태(이메일 알림 또는 대시보드 접근).
4. (선택) 등록 절차/접근 정보 내부 문서화: `docs/seo/search-console-setup.md`.

## Goal ancestry
SG-2 (한국어 패키징 핵심 50 키워드 SEO 점유율 40%) → P2.4. 자세한 내용: PACAA-25 plan v3 §3.

## 선행 / 후속
- 선행: 없음 (도메인 소유권만 필요).
- 후속: P2.5 (50 키워드 programmatic SEO 랜딩 페이지) — board sign-off 별도 필요.

## 비고
- 원래 Goal Owner는 CMO이지만 CMO 미채용 상태이며 본 작업은 기술 연동(도메인 verification, sitemap)이 핵심이라 Backend Engineer가 실행하고 추후 CMO 채용 시 운영 핸드오프.
- 도메인 verification 방식은 DNS TXT 레코드 우선(권장). 보드 승인 없이도 진행 가능한 두 방향 문(two-way door) 작업.

## Kill criterion
1주 내 양 엔진 verification 미완 → CTO escalate (도메인 권한 / DNS 접근 문제 가능성).
