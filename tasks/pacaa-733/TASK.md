---
name: "[Naver SEO] keywords.packlinx.com 웹 UI 사이트 등록 + sitemap 제출 (제휴 API skip)"
assignee: "ceo"
---

## 컨텍스트

PACAA-732 closeout 결정: Naver Search Advisor **API 통합은 skip** (제휴 API 승인 wall, P2). 대신 **웹 UI 기반 사이트 등록 + sitemap 제출**로 Naver 색인 가속화.

보드님이 이미 searchadvisor.naver.com 로그인 + 메뉴 탐색 가능 확인됨 (2026-05-16 스크린샷).

## Deliverable (CMO 진행, 보드 클릭만 위임)

### 1) 사이트 등록

- searchadvisor.naver.com → **사이트 관리** 탭 → **+ 사이트 등록**
- URL: `https://keywords.packlinx.com`

### 2) 소유 확인 (HTML 태그 방식)

- 화면에서 표시되는 `<meta name="naver-site-verification" content="..." />` 태그를 이슈 코멘트에 붙여주시면, CEO/CTO가 keywords 사이트 `<head>`에 박고 배포 → 보드님이 화면에서 "확인" 클릭

### 3) 사이트맵 제출

- 사이트 상세 → **요청** → **사이트맵 제출** → URL: `https://keywords.packlinx.com/sitemap.xml`
- 이미 사이트맵 200 OK 확인됨 (CEO 라이브 probe)

### 4) (선택) 메인 사이트도 같이

- `https://www.packlinx.com` 도 같은 절차로 등록 — Naver 색인 가속 (GSC는 이미 11.8만 페이지)

## Acceptance

- searchadvisor.naver.com 사이트 관리에 keywords.packlinx.com 등록됨
- 사이트맵 제출 상태 "성공" 표시
- 7~14일 후 Naver 검색 `site:keywords.packlinx.com` 으로 색인 결과 1+ 페이지 표시

## 우선순위 메모

- P1 (Naver 색인 자체는 시작되어야 SEO 노출 가능)
- 보드 클릭 5~10분, 그 외 agent 처리
- 막히는 화면 시 스크린샷 → 가이드 정정
