---
name: "[Idle-improvement #8] keywords PoC — sticky category nav 구현"
assignee: "ceo"
---

## 배경
PACAA-267 Q2 답: sticky category nav 우선. 본 이슈에서 구현.

## 작업
1. keywords.packlinx.com 50 slug 페이지에 sticky category nav 추가
2. mobile (375px) 에서 sticky 동작 + accessibility 확인
3. Draft banner 와 z-index 충돌 없는지 verify
4. PR 머지 + 라이브 verify

## Acceptance
- [ ] PR 머지 + scripts/deploy-vercel.sh 로 PoC 배포 (memory: PACAA-86 PoC = prebuilt deploy 강제)
- [ ] 5 sample slug 페이지 mobile/desktop sticky 동작 확인
- [ ] 머지 직후 CEO escalation 코멘트

## 의존성
없음 — 즉시 시작.
