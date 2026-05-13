---
name: "PACAA-626 P1 이미지 5장 페이지 적용 + 한국어 오버레이"
assignee: "frontend-engineer"
---

부모 PACAA-626 P1 이미지 5장이 머지 대기 branch 에 commit 됨. 각 페이지 컴포넌트에 적용 + 한국어 오버레이 + alt 텍스트 + LCP 측정.

## Branch
`feat/PACAA-626-ai-images-phase1` (origin push 완료). 이 branch 이어받아 작업 후 PR.

## 이미지 → 페이지 매핑
- `home-hero.webp` → `app/HomeHero.tsx` 또는 `app/page.tsx` hero section
- `guides-featured-trends.webp` → `app/guides/GuidesClient.tsx` featured #1 (2026 트렌드/규제)
- `guides-featured-eco.webp` → `app/guides/GuidesClient.tsx` featured #2 (친환경)
- `guides-featured-comparison.webp` → `app/guides/GuidesClient.tsx` featured #3 (박스 공급업체 비교)
- `match-hero.webp` → `app/match/page.tsx` hero

## 한국어 오버레이 (Option C — 보드 합의)
이미지에 한글 안 박힘. 페이지 코드에서 absolute/relative CSS 로 한국어 라벨 오버레이.
예: match-hero 위에 "공급업체 매칭" 헤드라인 (이미 페이지 헤더로 있으면 OK). guides featured 3카드는 카드 타이틀 그대로.

## Acceptance
- [ ] 5장 모두 next/image `<Image>` 컴포넌트로 적용 (priority 는 home-hero 만)
- [ ] 각 이미지 한국어 alt 텍스트 (예: home-hero alt="한국 패키징 업체 매칭 일러스트")
- [ ] LCP 측정: 적용 전후 PageSpeed 또는 Chrome DevTools 비교 (홈 페이지만)
- [ ] PR 만들고 CEO 머지 요청 (자동머지 아닌 ready_for_review 후 코멘트)

## 참고
- 비용 누계: $0.36 (Replicate Flux 1.1 Pro, P2 확장 시 추가 $0.40 예상)
- 이미지 brand 톤: 퍼플 그라데이션 #F0EEFF→#C4BAFF + #533AFD 액센트, isometric flat
- Phase 2 (카테고리 5 + 키워드 5) 는 P1 라이브 1주 GA4
