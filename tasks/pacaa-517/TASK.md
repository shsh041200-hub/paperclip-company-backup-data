---
name: "[CEO] PACAA-507 Phase B3 — vendor 운영 owner 워크플로우 SOP + criteria.md owner=CEO 갱신"
assignee: "ceo"
---

## 배경

[PACAA-507](/PACAA/issues/PACAA-507) 보드 결정: 운영 owner = CEO. LC §6 책무 7종 (부여·갱신·박탈·증빙 보존 등) 의 운영 SOP 정의 필요. 동시에 [PACAA-510](/PACAA/issues/PACAA-510) `docs/legal/vendor-verification-criteria.md` frontmatter `owner: Operations Lead (운영 owner, 미정 → CEO 지명 필요)` 를 `owner: CEO (Packlinx 대표)` 로 갱신.

## Acceptance

### Step 1. criteria.md frontmatter 갱신 (mechanical, ~5분)

- `docs/legal/vendor-verification-criteria.md` frontmatter `owner` 라인 → `owner: CEO (Packlinx 대표)`
- `revision: draft-r1` → `revision: r1` (보드 승인 표시)
- `status: 자문 초안 (Legal Counsel) — 보드 승인 전` → `status: 시행 (보드 승인 2026-05-11)`
- 본문 §6 의 "운영 owner (미정)" → "운영 owner: CEO"
- commit + PR. CEO 직접 머지.

### Step 2. 운영 SOP 문서 (`docs/legal/vendor-operations-sop.md` 신규)

LC §6 7종 책무 + 운영 흐름 명문화:

1. **신규 vendor 등록 시**: §1 5종 기준 검증 evidence 보존 절차 (현재 도구 / 데이터 위치 / 누가 입력)
2. **정기 갱신 (12개월)**: 캘린더 routine — Paperclip schedule 또는 calendar reminder
3. **이벤트 트리거 (vendor self-update / 도메인 변경 / 신고 누적)**: 모니터링 source + 응답 SLA
4. **박탈 결정 7종**: 단독 결정 권한 (CEO) vs LC 사전 검토 필요 분기
5. **vendor 통지**: 메일 템플릿 + 대시보드 표시 — PACAA-512 협업
6. **evidence 보존 3년**: 저장소 (DB 컬럼 vs S3 object) + 백업 정책
7. **공정위 자료 요구 15일 SLA**: escalation paths + Legal Coun
