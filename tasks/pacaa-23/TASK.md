---
name: "카테고리 개선 follow-up: /services/printing-design 진입점 추가"
assignee: "cto"
---

## 문제 (보드 제기)

PACAA-15에서 신설된 `/services/printing-design` 라우트가 **이용자 입장에서 발견 불가능**. 보드가 로컬 서버에서 직접 확인하며 "인쇄 디자인 관련 버튼도 안 보이고 들어가는 법도 모르겠다"고 보고.

원본 댓글: [PACAA-15#comment-de16b782](/PACAA/issues/PACAA-15#comment-de16b782-99df-47dc-af25-979c9cb5c2bb)

## 원인 가설

PACAA-16에서 라우트 자체는 만들었지만 **navigation surface에 진입점을 추가하지 않았음**. `/products/{slug}` 10종은 기존 카테고리 IA로 자연 진입되었을 수 있으나 `/services`는 새 축이라 별도 진입점 필요.

## Acceptance Criteria

다음 3개 surface 모두에서 `/services/printing-design`으로 진입 가능해야 함:

1. **글로벌 헤더 내비게이션** — Products와 동등한 위계로 Services 메뉴(또는 카드/링크) 노출. 데스크톱·모바일 양쪽.
2. **홈페이지** — Products 카드 그리드 옆/아래에 Services 섹션 또는 "인쇄·디자인" 카드. Buyer journey 분리 메시지가 드러나는 카피 권장(예: "패키지 인쇄·디자인이 필요하신가요?").
3. **`/products/{slug}` 페이지** — 관련 작업 흐름으로 "인쇄·디자인 서비스"로 cross-link(예: 페이지 하단 또는 사이드 패널). 패키징 발주 시 인쇄가 후속 흐름이라는 멘탈 모델 반영.

## Out of Scope

- Services 축 추가 라우트 신설 (현재는 printing-design 하나만)
- 디자인 시스템 변경
- 새로운 카피라이팅 작업 외 별도 카피 정련

## 검증

- `pnpm dev` 로컬에서 홈 → 서비스 진입 직접 확인
- 모바일 viewport(<768px)에서 동일 진입 가능 확인
- 빌드 + 타입체크 통과

## 의존

없음. `/services/printing-design` 라우트는 이미 존재.
