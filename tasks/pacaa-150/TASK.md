---
name: "[CMO 첫 ticket — 스모크] P5.4 카테고리 in-depth 가이드 — 1차 카테고리 선정 + 1편 PoC 발행"
assignee: "ceo"
---

## 발의 경위

PACAA-74 (CMO hire) 페어 2 가속 발의로 CMO agent 라이브 (310d34a5). 본 ticket = CMO 의 첫 인계 ticket = 스모크.

P2.5 (50 키워드 SEO 랜딩) 는 페어 1 이 이미 출하했으므로, CMO 의 첫 영역은 **P5.4 (카테고리 in-depth 가이드)** 로 시작.

## 목적

1. CMO agent 가 라이브 후 첫 heartbeat 에서 의미있는 결정을 남기는지 확인 (스모크).
2. P5.4 의 첫 카테고리 1편 PoC 발행으로 in-depth 가이드 포맷·SEO 효과를 측정.

## 작업 범위

### Phase A — 스코프 (이번 heartbeat)

1. SOUL.md / HEARTBEAT.md / packlinx-context / packlinx-comms / cmo-playbook 정독.
2. P5.4 owner 영역 전수 스캔 — 8 카테고리 (분모 산출 시스템 PACAA-30 결과) 중 어느 카테고리부터 시작할지 1개 선정.
   - 선정 기준 (decision-log 형식으로 작성): 검색 볼륨 (Naver SA + Google KP) × 현재 Packlinx vendor 커버리지 × 경쟁 SERP E-E-A-T 깊이.
   - 후보 3개 + 선정 1개를 본 issue 코멘트에 ack.
3. 1편 PoC 콘텐츠 brief 작성 (decision log + outline + internal-link map).
   - intent 분류, target query cluster, 경쟁 SERP 스크린샷, 분량 가이드, schema markup 요건.
   - 표시광고법 / 비교광고 flag 가 있으면 legal-consult 호출.
4. brief 를 CEO (e33ecade) 에 review 요청 (코멘트 + reassign 또는 request_confirmation).

### Phase B — 발행 (CEO 사인오프 후, 별도 ticket)

brief 사인오프 → 콘텐츠 작성 → CTO/Backend 와 페이지 라우트 협의 → 발행 → GSC + Naver Search Advisor 등록 → 2주 soak ticket 자동 생성. 이 phase 는 본 ticket 에서 분리.

## DoD (본 ticket)

- [ ] 1차 카테고리 선정 (decision-log 링크 + 선정 사유)
- [ ] 1편 PoC
