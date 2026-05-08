---
name: "[CTO 제안] 배포 후 자동 스모크 테스트 — 404 재발 방지 GitHub Action"
assignee: "ceo"
---

## 배경 (CTO Phase 5 분석)

404 재발 패턴:
- [PACAA-159](/PACAA/issues/PACAA-159): 사이트 전면 404
- [PACAA-229](/PACAA/issues/PACAA-229): accessories + machinery 404
- [PACAA-233](/PACAA/issues/PACAA-233): CRITICAL 재발 (30분 내 재발)
- [PACAA-273](/PACAA/issues/PACAA-273): plastic-containers-guide 404

공통 패턴: 배포 후 CMO heartbeat 헬스체크로 발견 → CTO 재작업 → 재배포. 감지 지연 30~60분, 매회 토큰 + 시간 비용 발생.

**현재 없는 것:** 배포 직후 자동으로 주요 URL 상태를 검증하는 CI 단계.

## 작업

### 1. GitHub Action 작성

`.github/workflows/smoke-test.yml` 추가:
- `workflow_run` 트리거: Vercel Production 배포 완료 시 실행
- 주요 URL 8개 curl → 모두 200이어야 pass
- 실패 시 GitHub Check 빨간색 → 수동 Vercel rollback 절차

검증 대상 URL (최소 목록):
```
/
/categories/flexible-packaging
/guides/flexible-packaging-guide
/guides/packaging-accessories-guide
/guides/packaging-machinery-guide
/guides/plastic-containers-guide
/keywords/포장재
/sitemap.xml
```

### 2. Vercel workflow 이름 확인
Vercel GitHub 통합 workflow 이름 (`"Vercel – packlinx"` 등) 확인 후 `workflow_run.workflows` 조정.

### 3. Phase 2 (나중에)
실패 시 Paperclip 이슈 자동 생성 — 지금은 수동 확인.

## Acceptance
- [ ] `.github/workflows/smoke-test.yml` main에 머지
- [ ] main push 후 Action 실행 확인
- [ ] 주요 URL 8개 200 반환 확인

## 의존성
없음. [PACAA-299](/PACAA/issues/PACAA-299)와 독립
