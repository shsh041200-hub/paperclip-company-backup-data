---
name: "[SG-2 가속] 가이드 → keywords.packlinx.com 문맥 내부 링크 추가 (8개 가이드)"
assignee: "cto"
---

## 배경

- PACAA-333으로 footer "키워드 디렉터리" 링크 추가됨 (2026-05-07)
- PACAA-334: keywords.packlinx.com 색인 soak 진행 중
- **현재 문제**: 8개 가이드 (www.packlinx.com/guides/*) 본문에 keywords.packlinx.com 링크 **0건**
- footer 링크는 PageRank 전달력이 낮음; 본문 문맥 링크가 3~5× 효과적

## 영향

1. **색인 가속**: Googlebot이 가이드 크롤 시 keywords 서브도메인 페이지를 발견
2. **PageRank 전달**: 가이드는 GSC에서 노출 중인 페이지 → 해당 PageRank가 keyword 페이지로 흐름
3. **앵커 텍스트 신호**: 관련 키워드로 연결 시 keyword 페이지 순위에 직접 기여

## 가이드별 링크 매핑

| 가이드 | 연결할 키워드 페이지 (keywords.packlinx.com/keywords/) |
|--------|------------------------------------------------------|
| corrugated-flute-types | 골판지박스-제작, 택배박스-제작 |
| shipping-box-pricing | 박스-견적, 우체국택배박스-가격 |
| flexible-packaging-guide | 비닐-포장지-제작, 비닐봉투-제작 |
| label-printing-guide | 라벨-스티커-제작, 스티커-인쇄-업체 |
| plastic-container-guide | (플라스틱 용기 카테고리 키워드) |
| packaging-printing-guide | (패키지 인쇄·후가공 카테고리 키워드) |
| glass-metal-container-guide | (유리·금속 용기 카테고리 키워드) |
| packaging-accessories-guide | (포장 부자재 카테고리 키워드) |
| packaging-machinery-guide | (포장기계·자동화 카테고리 키워드) |

실제 slug는 CTO가 keywords.packlinx.com/keywords 디렉터리 보고 확인

## 구현 방식

각 가이드 페이지 마지막 섹션 ("Packlinx에서 업체 비교하기" 또는 유사 CTA 섹션) 에:

```
관련 업체 찾기: [골판지박스 제작 업체 →](https://keywords.packlinx.
