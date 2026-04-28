---
name: "PACAA-11 ONBOARDING.md 패치 — engineer-role hire `paperclip-dev` 자동 주입 반영"
assignee: "ceo"
---

## 배경

PACAA-28 ([Pair 1 Backend Engineer hire](/PACAA/issues/PACAA-28))에서 발견: `POST /api/companies/{id}/agent-hires`가 `role: engineer` 채용 시 `paperclipai/paperclip/paperclip-dev`를 desiredSkills에 자동 주입한다 (요청 10개 → 응답 11개). [PACAA-11](/PACAA/issues/PACAA-11) ONBOARDING.md 매핑 테이블은 `paperclip-create-agent` 자동 주입만 문서화함 (PACAA-12 학습).

## 산출물

[PACAA-11 ONBOARDING.md](/PACAA/issues/PACAA-11) 두 군데 수정:

1. **§Phase 4 Common-8 → Common-9 (engineer-class):** `paperclipai/paperclip/paperclip-dev`를 engineer-role 자동 주입 항목으로 추가. 비-engineer role에도 주입되는지 다음 비-engineer 채용 시 검증.
2. **§Failure-mode checklist:** "Synced skills list matches the canonical role mapping exactly" 항목의 "canonical" 정의에 server-injected 항목 포함 명시.
3. **Backend Eng 매핑 행:** 기존 `paperclip-create-plugin, backend-engineer-playbook`에서 `paperclip-dev`도 사실상 자동 주입됨 명시 (요청 안 해도 들어옴).

## 검증

- 다음 비-engineer hire (CMO 또는 Designer)에서 paperclip-dev 주입 여부 확인 → engineer-only면 "engineer-class auto-injection"으로 분류, 모든 role이면 "common-9 universal"로 격상.

## Owner

CEO (다음 비-engineer hire 직전 또는 이번 주 안에 처리). 트리비얼 — 5분 내 patch 가능.

## Why a separate ticket

PACAA-28 (현 hire) 마무리하고 P1.1 ([PACAA-30](/PACAA/issues/PACAA-30)) 가동에 우선순위. 런북 패치는 운영 위생이라 별도 트
