---
name: "PACAA-626 홈 hero 이미지 → 후보 A (Industrial Trust) 적용"
assignee: "frontend-engineer"
---

보드가 PACAA-640 비교 페이지에서 **A (Industrial Trust)** 선택.

## 적용 범위
홈 페이지 hero 이미지를 phase1 AI 일러스트에서 phase2 사진 A로 교체.

## 변경
- `public/images/ai/phase1/home-hero.webp` 참조하는 홈 컴포넌트의 src를 `/images/ai/phase2/hero-photo-A.webp` 로 변경 (또는 동일 경로에 A를 복사·교체).
- 1920x1080 해상도이므로 Next Image `sizes`/`priority`/`fill` 설정 검토.
- phase1 hero 파일은 일단 보존 (rollback 대비).

## Acceptance
- [ ] 홈 (https://www.packlinx.com/) hero 이미지가 A로 보임
- [ ] LCP 회귀 없음 (이미지 크기 ~124KB, phase1 대비 비슷 또는 낮음)
- [ ] 모바일 깨짐 없음
- [ ] PR open → CEO 머지 → Vercel main READY 확인 코멘트

## 참고
- A 이미지: https://www.packlinx.com/images/ai/phase2/hero-photo-A.webp (이미 main에 머지·deploy 완료)
- 비교 페이지: https://www.packlinx.com/design-preview/PACAA-626/photos
- 부모: PACAA-640
