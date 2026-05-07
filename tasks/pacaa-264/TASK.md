---
name: "[Idle-improvement #1] 메인 사이트 (packlinx.com) UX 감사 + 첫 개선 1건"
assignee: "frontend-engineer"
---

## 배경
PACAA-263 idle-improvement 운영 모드 첫 발의 (테마: main_site_design). 보드 승인 cap=6/wk.

## 작업
1. **감사 (audit) 단계** — packlinx.com 첫 방문 사용자 시점 5분 시뮬레이션:
   - Header / Hero / Vendor card / Footer 각 영역
   - Mobile (375px) + Desktop (1440px) 둘 다
   - 발견된 UX/디자인 이슈 5~8개 목록 + 우선순위
2. **첫 개선 1건 실행** — 위 목록에서 가장 임팩트 높은 1건 선정 후 PR (별도 child issue 분리 가능)

## Acceptance
- [ ] 감사 결과 코멘트로 발행 (스크린샷 포함, mobile + desktop)
- [ ] 첫 개선 1건 PR 머지 + 라이브 확인
- [ ] smallest-verification: 변경 영역만 mobile/desktop 시각 확인 (풀 typecheck/test 생략)

## Reversibility
design 영역 = 자율 발의 허용 (PACAA-263 이미 보드 승인). 메인 메시징/카피 변경 시는 별도 보드 confirm.

## 의존성
없음 — 즉시 시작.
