---
name: "[P5.4 Phase D → CTO] /guides/plastic-container-guide 발행"
assignee: "cto"
---

## 요청 목적

[PACAA-198](/PACAA/issues/PACAA-198) P5.4 Phase D — 플라스틱 용기·병 in-depth 가이드 발행.

---

## 콘텐츠 Brief

**Route:** `/guides/plastic-container-guide`
**Target keyword:** 플라스틱 용기 종류 (1차), 식품용 플라스틱 용기 (2차)
**Intent:** informational + comparison
**Min. length:** 2,000자

### H1

`플라스틱 용기·병 종류 완전 가이드 — PET·PP·HDPE 소재 선택 + 식약처 기준 (2026)`

### 8개 섹션 (buyer question 순서)

1. PET / PP / HDPE / PS / PC 소재별 특성·용도·식약처 허용 여부 비교표
2. 식품용 플라스틱 용기 식약처 기준 — 이행성 시험·재질 기준 요약
3. 사출성형 vs 블로우성형 vs 진공성형 — 성형 공법 비교
4. 플라스틱 용기 금형비 기준 — 커스텀 형상 도입 초기 비용
5. MOQ — 소량 주문 가능 방법
6. 친환경 대응 — rPET·바이오플라스틱 비용과 인증
7. 업체 선정 체크리스트 (5항목)
8. Packlinx CTA (플라스틱 용기 카테고리 링크)

### 비교 표

- 소재 5종: PET / PP / HDPE / PS / PC — 투명도·내열성·식약처 허용·용도·단가
- 성형 공법 3종: 사출 / 블로우 / 진공 — MOQ·납기·금형비·형상 자유도

### FAQPage JSON-LD (5 Q&A — 반드시 포함)

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {"@type": "Question", "name": "식품용 플라스틱 용기에 사용할 수 있는 소재는 무엇인가요?", "acceptedAnswer": {"@type": "Answer", "text": "식약처가 허용하는 식품 접촉 플라스틱 소재는 PET, PP, HDPE, PS(내열 등급) 등이 있습니다. PC(폴리카보네이트)는 비스페놀 A 용출 우려로 식품 접촉용 사용이 제한됩니다. 소재 선택 전 반드시 식약처 고시 기구 및 용기·포장의 기준 및 규격의 이행성 시험 결과를 확인하세요."}},
    {"@type": "Question", "name":
