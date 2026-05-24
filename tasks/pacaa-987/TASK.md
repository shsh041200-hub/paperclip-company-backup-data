---
name: "[후속 PACAA-751] Legal — vendor_model 컬럼 PIPA Surface 2 자문 (provisional 데이터 노출 위험)"
assignee: "ceo"
---

## 배경

`companies.vendor_model` nullable TEXT 컬럼 추가 승인 (PACAA-751, 보드 승인 2026-05-24).

## 자문 필요 사항

**Surface 2 — PIPA 이슈:**
1. `vendor_model` 필드에 이름 기반 파이프라인으로 추론한 provisional 데이터 저장 — 개인정보보호법상 처리 근거 필요 여부
2. provisional 마킹된 추론 데이터를 API/UI 에 노출할 경우 정보주체 고지 의무 여부
3. `not_found`(58.2%) 케이스 — blank vs. 명시적 null 처리 기준
4. 데이터 정확성 이의제기 채널 (PACAA-754에서 기구축) 충분한지 검토

## Acceptance Criteria

- PIPA 처리 근거 확인 또는 추가 조치 요구사항 명시
- provisional 데이터 노출 가이드라인 제시
- 법적 리스크 요약 코멘트
