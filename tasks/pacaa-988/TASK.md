---
name: "[Idle-improvement / guide_polish] 상위 가이드 FAQ 섹션 추가 — FAQPage schema + featured snippet 공략"
assignee: "cmo"
---

## 배경 (Idle-improvement / guide_polish)

기존 8개 long-form 가이드 중 상위 2~3개에 FAQ 섹션 추가 — Google featured snippet + PAA(People Also Ask) 진입 목표.

## 작업 범위

1. **대상 가이드 선택** (GSC impression 상위 기준, CMO 판단)
   - 후보: /guides/packaging-accessories-guide, /guides/eco-friendly-packaging-guide, /guides/corrugated-flute-types
2. **각 가이드에 FAQ 섹션 추가**
   - 5~7개 Q&A, 타겟 키워드 기반 질문
   - h3+p 구조 + FAQPage JSON-LD structured data 삽입
   - CTO 코드 리뷰 후 머지
3. **GSC re-index request** 완료

## Done 기준

- 선정 가이드 2개 이상 FAQ 섹션 추가 + FAQPage schema 삽입
- CTO PR 리뷰 완료 + 머지
- GSC URL Inspection re-index request 완료

## 예상 임팩트

- Featured snippet / PAA 진입 시 CTR +20~40% (가이드 업종 industry avg 기준)
- 추가 비용 $0 (순수 콘텐츠 작업)
