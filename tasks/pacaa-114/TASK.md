---
name: "GSC 4xx 5,667페이지 진단 + 4/25 폭증 root cause"
assignee: "ceo"
---

## 배경

PACAA-113 ([plan](/PACAA/issues/PACAA-113#document-plan)) 의 P0 트랙. 보드 승인 완료.

GSC 색인 리포트(4/27 기준):
- 알려진 페이지: 25,029 / 색인된 페이지: 6,567 (26%)
- **5,667 페이지가 4xx로 차단됨**
- **4/24→4/25 사이 알려진 페이지 3,697 → 25,029 (~7배 폭증)** ← 이 시점에 무엇이 변했는지 파악이 진단의 출발점

원본 GSC export 4종은 PACAA-113 첨부 참조 (차트.csv / 메타데이터.csv / 심각한 문제.csv / 중요하지 않은 문제.csv).

## 요청 작업

### Task A — 5,667 4xx URL 패턴 진단
1. GSC에서 4xx URL 샘플 추출 (Search Console Index → 페이지 → "다른 4xx 문제로 인해 차단됨" 클릭 → URL 목록 export)
2. URL 패턴 분류 (예: `/vendor/{slug}` 삭제 케이스, 필터 조합, 인증 게이트, 깨진 리다이렉트)
3. 사이트맵에 포함되어 있는지 / 내부 링크에서 생성되는지 분류
4. 산출물: 패턴 ≤ 5종 + 각 패턴별 페이지 수 + 1줄 fix 방향

### Task B — 4/25 변화 root cause
1. 4/24 18:00 ~ 4/25 24:00 (KST) 사이의 배포 / 데이터 import / sitemap 생성 변경 추적
2. 가설: sitemap 생성 로직 변경, 신규 데이터 import (벤더 ~21,000 추가?), URL 패턴 변경
3. 산출물: root cause 1줄 + 그 변화가 의도된 것이었는지 + 되돌릴지 / 보정할지 판단

## 제약 / 컨텍스트

- **Backend Engineer 가 현재 `error` 상태** — Task B는 원래 Backend 영역이지만 CTO가 흡수 가능. Backend 복구가 빠르게 되면 위임 가능.
- 운영 도메인 / GSC 권한이 필요하면 본 이슈 코멘트로 요청 → CEO가 보드에 에스컬레이션.
- 가역성: 분석 단계라 모두 two-way door. 수정 액션은 별도 child issue로 분리.

## 예상 ROI / 마감

- Task A 산출물 → 사이트맵 정화 (P1) 의 입력
- Task B root cause → 폭증 자체를 되돌릴지 결정 (만약 의도되지 않았으면 즉시 롤백)
- 이번 주
