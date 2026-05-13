---
name: "PACAA-626 홈 hero 실사 사진 3개 후보 생성 + 비교 페이지"
assignee: "ceo"
---

홈 hero 이미지를 실사 사진으로 교체. 변경안 3가지를 라이브 비교 페이지로 띄워 보드 선택을 받기 위한 후보 생성.

## 보드 요청
- 현재: AI 일러스트 (1344x768, `/images/ai/phase1/home-hero.webp`)
- 변경: 실사 사진, 해상도 향상

## 생성할 3개 후보 — 모두 실사 사진 (photorealistic)

각각 1920x1080 (16:9) WebP, 품질 90, 200KB 이하 목표. `/match-hero.webp` 가 480px height + full-width + 좌측 gradient overlay 위에 표시되므로 **좌측 영역은 비교적 비워두고 우측/중앙에 시각적 임팩트** 배치 (gradient overlay 가 카피 가독성 보장하도록).

### 후보 A — 한국 패키징 공장 작업장
**Replicate Flux 프롬프트** (영어):
```
Photorealistic wide-angle photo of a modern Korean packaging factory floor, conveyor belt with stacked cardboard boxes moving through, a worker's hands close-up wrapping a box with kraft paper, natural daylight from large windows on the right, soft warm lighting, professional B2B industrial atmosphere, clean and organized workspace, shallow depth of field, color graded with warm earthy tones, 35mm lens look, high detail, no faces visible, no text
```
- 저장 경로: `public/images/ai/phase2/hero-photo-A.webp`
- 컨셉 키워드: **전문성·신뢰감 (Industrial Trust)**

### 후보 B — 포장 제품 스튜디오 진열
**Replicate Flux 프롬프트**:
```
Photorealistic studio product photography of an assortment of premium packaging boxes and containers arranged neatly on a soft cream grad
