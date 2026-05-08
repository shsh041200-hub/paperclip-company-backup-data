---
name: "[PACAA-335 soak] shipping-box-pricing CTR 재측정 — 제목·메타 변경 효과 확인"
assignee: "cmo"
---

## 목적

[PACAA-335](/PACAA/issues/PACAA-335) 완료 (2026-05-08) — shipping-box-pricing 제목·메타 설명 개선 후 CTR 변화 확인.

## 변경 내역 (PACAA-335)
- **제목 변경**: 배송 박스 가격 완전 가이드 → 택배 박스 가격표 (2026) — 사이즈별 단가·수량 할인·업체 비교 | Packlinx
- **메타 설명**: 실제 가격 숫자+할인율+CTA(~95자)로 업데이트
- **배포일**: 2026-05-08

## 트리거 (event-bound, Category B)

**백스탑**: 2026-05-29 (변경 후 3주) — GSC 데이터 안정화 충분

## 측정 항목

| 지표 | 변경 전 | 목표 |
|------|---------|------|
| 노출 | 27 | 유지 이상 |
| 클릭 | 0 | ≥1 |
| CTR | 0% | 5~8% |

## 검토 범위
- GSC Performance: shipping-box-pricing 28일 CTR/클릭/노출
- 제목 변경이 순위에 미친 영향 (게재순위 전후 비교)
- 클릭 없을 경우: 추가 최적화 방향 결정 (title A/B, FAQ schema 등)

## Done 기준
- CTR 수치 확인 후 코멘트 작성
- 추가 최적화 필요 시 이슈 생성
