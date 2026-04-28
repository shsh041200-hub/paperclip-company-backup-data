---
name: "Pair 1 채용 — Backend Engineer (SG-1 owner)"
assignee: "ceo"
---

## 배경 (Why hire, why now)

[PACAA-26](/PACAA/issues/PACAA-26) 사인오프 완료 (2026-04-28 07:59 UTC).
이로써 SG-1 (8개 우선 카테고리 vendor 등록률 90%) 하위의 P1.1\~P1.4
실행 게이트가 풀림. P1.1 (8개 카테고리 분모 산출 시스템)부터 시작
가능 — 단, **owner가 없음**. PACAA-25 plan v3 §5 채용 시퀀싱에 따라
**Pair 1 \= Backend Engineer 단독** 채용을 즉시 진행.

## 채용 결정 사항 (이미 보드 사인오프됨)

PACAA-25 plan v3 §5 + 보드 사인오프 코멘트로 확정된 항목:

* **Role:** Backend Engineer
* **Adapter:** `claude_local`
* **Model:** **Sonnet 4.6** (Opus 토큰 prioritization 정책상 IC 역할은
  Sonnet)
* **ReportsTo:** CEO (현 시점 CTO 외 다른 manager 없음)
* **Pair sequencing:** Pair 1 단독 채용 (안정화 2\~3주 → Pair 2 \= CMO +
  Frontend Eng 동시 채용)

## 책임 범위

PACAA-25 plan v3 §5 정의:

* **SG-1 owner**: 8개 우선 카테고리 vendor 등록률 90% (3개월).
* **Project Goals 직접 owner:**
  * P1.1 8개 카테고리 분모 산출 시스템 (2주)
  * P1.2 카테고리별 vendor target list 수집 (2주, P1.1 후)
  * P1.3 dedup + canonicalization 파이프라인 (1주)
  * P1.4 profile 완전성 감사 (2주)
* **공동:** P4.3 Vendor 자기-노출 분석 화면 일부 (Frontend Eng와 협업,
  Pair 2 시작 후)
* **Cross-cut:** CTO와 데이터 레이어 협업 (SG-3 측정 인프라가 P1.1
  분모 산출과 데이터 모델 공유).

## Day-1 skills (canonical 매핑)

PACAA-8 common 7개 + role specialty:

* `paperclip-create-plugin` (Backend Eng는 plugin 작성 권한)
* `backend-engineer-playbook`
*
