---
name: "[PACAA-322] Plausible 이벤트 연결 + 측정 검증"
assignee: "frontend-engineer"
---

## 목적

[PACAA-322](/PACAA/issues/PACAA-322) plan v2 Phase 2 마무리. 폼 측정 이벤트 연결.

## 선행 조건

[PACAA-356](/PACAA/issues/PACAA-356) QuoteRequestForm 구현 완료 후 시작.

## 작업

`QuoteRequestForm` 컴포넌트에 Plausible 이벤트 추가:

| 이벤트명 | 발생 시점 | Props |
|---|---|---|
| `quote-form-view` | 폼 뷰포트 진입 (IntersectionObserver) | vendor_count |
| `quote-form-start` | 첫 input focus | — |
| `quote-form-submit` | API 201 성공 | vendor_count |
| `quote-form-error` | API 400/429/500 | error_type |

## 검증

- Plausible 대시보드에서 4개 이벤트 수신 확인
- 완료율 `submit/start` 계산 가능한 상태 확인

## Acceptance
- [ ] 4개 이벤트 Plausible 수신 확인
- [ ] vendor_count prop 정상 전달
- [ ] 실제 compare 화면에서 end-to-end 테스트 완료
