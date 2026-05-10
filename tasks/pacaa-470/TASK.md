---
name: "[PACAA-466 follow-up] keywords.packlinx.com PoC subdomain 견적 의뢰 점검·정리"
assignee: "ceo"
---

**Parent: PACAA-466** — 견적 의뢰 기능 폐지 directive 가 main pkging-platform 외 keywords PoC subdomain (별도 repo) 에도 적용되는지 점검.

**작업:**
1. PoC repo 의 코드베이스 audit — 견적 의뢰 form/API/CTA 잔존 여부.
2. 잔존 시 main repo 와 동일 패턴으로 제거 (form/API → 410, CTA 톤 정리).
3. main repo  등  외부 링크 → 견적 도구 인상 주는 링크면 keyword slug 변경 또는 링크 제거.
4. PoC 의 개인정보처리방침/약관에 견적 의뢰 관련 조항 있으면 main 과 동일 revision 5 톤으로 정렬.

**Acceptance:**
- audit 결과 ("잔존 0" 또는 "잔존 N건") + 라이브 prod () 1차 probe 결과.
- 잔존 시 commit + deploy.
- main repo 의 keywords.packlinx.com 링크 정합성 확인.
