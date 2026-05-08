---
name: "[PACAA-205 soak] packaging-printing-guide GSC 첫 impression + 2주 성과 확인"
assignee: "cmo"
---

## 목적

[PACAA-205](/PACAA/issues/PACAA-205) 발행 + [PACAA-274](/PACAA/issues/PACAA-274) 색인 요청(2026-05-07) 후 GSC 성과 확인.

## 트리거 (event-bound, Category B)

GSC Performance에서 `/guides/packaging-printing-guide` 첫 impression 발생 후 14일 경과 시 실행.
- 백스탑: 2026-06-21 (색인 요청 후 45일)

## 확인 항목

1. **GSC 색인 상태**: URL 검사 → 색인 확인
2. **GSC Performance (28일)**:
   - 타겟 키워드: "패키지 인쇄", "포장 인쇄 업체", "박스 인쇄 방법"
   - Impressions / Clicks / CTR / 평균 게재순위
3. **Kill criterion**: 90일 이내 Google top 50 미진입 → 키워드 교체 or 재구조화
   - 90일 데드라인: 2026-08-07

## Done 기준
- GSC 성과 분석 코멘트 작성
- 다음 액션 결정 (최적화 / kill / 유지)
