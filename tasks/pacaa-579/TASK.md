---
name: "D1 — Vendor slug↔entity 정합성 audit + 정리"
assignee: "ceo"
---

## 배경

PACAA-573 보드 directive (코멘트 `dc272aad`): C2 제외 후속 우선순위 전부 진행. D1 = vendor URL slug 와 실제 vendor entity 정합성 audit + 정리.

## 목표

vendor 페이지 URL slug (예: `/vendors/{slug}`) 와 DB vendor record 이름/식별 정합성 불일치 케이스 발굴 → 정정 (rename / redirect / dedup). SEO 신뢰도 + 사용자 confusion 감소.

## 작업 — 2단계 (audit 먼저, mutation 후속)

### Phase 1 — audit only (이 이슈 1차 closeout)

1. DB 의 vendors 테이블 슬러그/이름 전수 sweep (read-only)
2. 의심 케이스 분류:
   - (A) slug 와 vendor 이름 한자/한글 변환 mismatch
   - (B) 같은 vendor 가 다른 slug 로 중복 등록 (dedup 후보)
   - (C) slug 가 placeholder/test 패턴 (예: `vendor-1`, `test-slug`)
3. 영향 vendor 수 + 카테고리별 분포 + production URL 200/404 check
4. 본 이슈 코멘트에 audit 결과 표 + 정정 옵션 (B/C-만 처리, A-도 포함, 또는 보수적 skip)
5. CEO 에 escalation → 보드 결정 ask 발의

### Phase 2 — mutation (보드 accept 후 별도 child)

- redirect / rename / dedup 마이그레이션 — DB 변경 위험 audit 통과 후만
- 기존 슬러그 → 301 redirect 보존 (SEO 손실 방지)

## Acceptance — Phase 1

- [ ] audit 결과 표 (영향 수 + 카테고리)
- [ ] 정정 옵션 3안 surface
- [ ] CEO escalation 코멘트

## 참고

- 메모리: feedback_introspect_prod_schema_before_create (read-only sweep 도 라이브 introspect)
- 메모리: feedback_subagent_immediate_escalation (Phase 1 끝나면 in_review 발의 + CEO 명시 에스컬레이션)
- Phase 2 는 prod data mutatio
