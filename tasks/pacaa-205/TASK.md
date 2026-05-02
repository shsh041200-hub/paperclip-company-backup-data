---
name: "[P5.4 Phase E → CTO] /guides/packaging-printing-guide 발행 (인쇄·후가공)"
assignee: "cto"
---

## 목적

P5.4 8개 카테고리 가이드 중 5번째: 인쇄·후가공(printing & post-processing) in-depth 가이드 발행.

## 카테고리 선택 근거

- 인쇄·후가공은 박스·라벨·연포장재 등 모든 포장재에 공통 적용되는 B2B 구매 결정 요소
- '포장 인쇄 업체', '후가공 종류', '코팅 종류' Naver 검색량 높음
- PACAA-86 랜딩 페이지(인쇄·후가공 키워드)로의 가이드 유입 → vendor 클릭 전환

## 가이드 사양

**Route:** `/guides/packaging-printing-guide`
**Target keyword:** 포장 인쇄 종류 (1차), 포장 후가공 종류 (2차)
**Min. length:** 2,000자

### 8개 섹션

1. 포장 인쇄 방식 종류 — 옵셋 / 플렉소 / 그라비어 / 디지털 비교표 (MOQ·단가·납기·색재현)
2. 포장재별 적합 인쇄 방식 (골판지 / 연포장재 / 라벨 / 종이백)
3. 후가공 종류 — 코팅(유광/무광/UV) / 박(금박/은박) / 엠보싱 / 형압 / 창문 후가공
4. 인쇄 색상 관리 — CMYK vs 별색(Pantone), 색상 재현 정확도
5. 식품 포장 인쇄 잉크 규제 — 식약처 기준 + EU/FDA 대응
6. 인쇄 파일 규격 — 블리드·해상도·컬러모드 준비 체크리스트
7. 업체 선정 체크리스트 (5항목)
8. Packlinx 인쇄·후가공 업체 CTA

### FAQPage JSON-LD (5 Q&A)

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {"@type": "Question", "name": "포장 인쇄 방식 중 소량 주문에 가장 적합한 것은 무엇인가요?", "acceptedAnswer": {"@type": "Answer", "text": "소량(500장 미만) 인쇄에는 디지털 인쇄가 가장 적합합니다. 판(plate) 제작 비용이 없고 납기가 1~3 영업일로 짧습니다. 단, 장당 단가가 옵셋·플렉소보다 높아 수천 장 이상부터는 옵셋이나 플렉소를 검토하는 것이 경제적입니다."}},
    {"@type": "Question", "name": "유광 코팅과 무광 코팅은 어떤 차이가 있나요?", "acceptedAnswer": {"@type": "Answer", "text": "유광
