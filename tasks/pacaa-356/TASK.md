---
name: "[PACAA-322] QuoteRequestForm 컴포넌트 — 2개 PIPA 동의 체크박스 + 고지문"
assignee: "frontend-engineer"
---

## 목적

[PACAA-322](/PACAA/issues/PACAA-322) plan v2 Phase 2. 견적 의뢰 폼 UI.

## 선행 조건
[PACAA-355](/PACAA/issues/PACAA-355) API 완료 후 시작.

## 작업

**컴포넌트:** app/components/QuoteRequestForm.tsx

폼 구성:
1. 헤더: '선택한 업체에 한번에 견적 요청하기'
2. 선택된 vendor 3사 명칭 칩 (읽기 전용 — §17 제공받는 자 특정 필수)
3. 이메일 input (필수)
4. 회사명 input (선택)
5. 수량·요구사항 textarea (필수, min 10자)
6. 납기 date input (선택)
7. Honeypot hidden input (_honey)

PIPA 동의 영역 (묶음 금지 §22(3)):
- [필수] 체크박스1: 개인정보 수집·이용 동의 §15 + 전문 아코디언
- [필수] 체크박스2: 제3자 제공 동의 §17 + 전문 아코디언 (vendor 사명 포함)
- 고지문 (텍스트): 'Packlinx는 통신판매중개자로서 견적 의뢰의 당사자가 아닙니다'
- 제출 버튼 #533afd Primary CTA
- 성공 화면

**compare 페이지 통합:**
app/compare/page.tsx — tfoot 아래, CompareCart 위에 삽입. companies.length===0 미노출.
compare 페이지 footer에도 통신판매중개자 고지문 (§20).

**디자인:** DESIGN.md 필수 준수 (#533afd CTA, #061b31 헤딩, radius 4-8px)

## Acceptance
- [ ] 체크박스 2개 분리 각 independently required
- [ ] vendor 사명 폼 상단 노출
- [ ] 고지문 비교페이지+폼 내 노출
- [ ] DESIGN.md 준수
