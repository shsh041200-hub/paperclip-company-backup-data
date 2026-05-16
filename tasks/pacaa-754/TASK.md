---
name: "[후속 PACAA-737] FE+BE 이의제기 채널 implementation (Legal SLA PACAA-750 spec — 폼+이메일+page링크+audit 5년+admin tool)"
assignee: "frontend-engineer"
---

**부모**: PACAA-737 (보드 옵션 B 결정 = 통지 생략 + 이의제기 채널만). PACAA-750 Legal SLA spec implementation.

## 옵션 B 의 안전망 (Legal good faith 입증 핵심)
보드가 launch 통지 생략 결정 → 이의제기 채널이 **유일한** 분쟁 처리 인프라. 채널 quality 가 Legal risk 직결.

## 작업 범위 (Legal PACAA-750 spec 기반)

### 1. 이의제기 웹폼 (`/vendor/dispute`)
- 식별 필드 (vendor name, 사업자등록번호, 담당자 연락처)
- 분쟁 사유 dropdown (분류 오류 / 정보 부정확 / 삭제 요청 / 기타)
- 첨부파일 (통신판매업 신고증 등)
- 자동 접수번호 발급 + vendor 에게 확인 이메일

### 2. 이메일 백업 채널 (`vendor-support@packlinx.com`)
- 폼 접근 어려운 vendor 백업
- 라우팅 = admin tool 큐에 자동 등록

### 3. Page-level 정정 요청 링크 (옵션 B 핵심)
- `/internal/vendor-redesign/v1/[slug]` (그리고 launch 후 메인 라우트) 페이지 footer 에 "분류 정정 요청" 작은 링크
- 클릭 → `/vendor/dispute` 폼 + vendor_id prefill

### 4. Audit 로그 schema (5년 보존)
- 새 테이블 `vendor_classification_disputes`
  - id, vendor_id, submitted_at, channel (form/email), reason, status (접수/검토중/정정완료/유지), before/after classification, resolved_at
- 새 테이블 또는 trigger `vendor_classification_audit`
  - id, vendor_id, before_model, after_model, changed_by, changed_at, reason
- 보존 정책: 5년 후 자동 익명화 (vendor_id null, 나머지 통계용 보존)

### 5. Admin tool 검토 UI
- `/admin/disputes` — 큐 리스트 + 상세 검토 + 정정/유지 처분
- SLA tracking: 영업일 14일 1차 회신, 30일 최종 처분 — 임박 알림

##
