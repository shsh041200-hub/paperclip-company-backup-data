---
name: "PACAA-452 FE (재발의) — batch 4 4개 가이드 v1 슬롯 fresh PR (latest main)"
assignee: "frontend-engineer"
---

## 목적
PACAA-420 가이드 v1 템플릿 마지막 배치 (4개 가이드) FE 구현. 이전 FE child PACAA-454/455 는 mergeable=dirty (stale base) 로 둘 다 cancelled.

본 ticket = **단일 깔끔 PR**. latest `main` 기준으로 작업.

## 콘텐츠 소스 (4개 가이드)
모두 PACAA-452 inline 코멘트에 풀 텍스트 (TL;DR · Callout · Checklist · FAQ · Sidebar · end-CTA 6슬롯) 있음. **Legal Counsel 자문 PASS, 수정 권고 없음 — 초안 그대로 최종본**.

1. `packaging-printing-guide` — [PACAA-452 #515b91aa](/PACAA/issues/PACAA-452#comment-515b91aa)
2. `packaging-machinery-guide` — [PACAA-452 #649c1c6c](/PACAA/issues/PACAA-452#comment-649c1c6c)
3. `packaging-tape-comparison` — [PACAA-452 #0d8f1733](/PACAA/issues/PACAA-452#comment-0d8f1733)
4. `2026-korea-packaging-trends` — [PACAA-452 #7d5a6402](/PACAA/issues/PACAA-452#comment-7d5a6402) ⚠️ HIGH-risk: 정식 법령명 「자원의 절약과 재활용촉진에 관한 법률」 + EPR 분담금 단가 단정 금지 + KPRC/환경부 공지 확인 안내

## 작업 절차

1. `git checkout main && git pull` — latest main 부터 fresh branch (`feat/PACAA-456-batch4-final`)
2. **수정 파일 — 최소 1~2개 만**:
   - `app/guides/[slug]/page.tsx` — GUIDES record 에 4개 entry 추가 (배치 3 의 glass-metal/packaging-accessories 마이그레이션 패턴 그대로)
     - `redesignVersion: 1` 명시
     - `body` 함수에 v1 슬롯 컴포넌트 (`GuideHero` TL;DR · `GuideCallout` × N · `GuideChecklist` · `GuideFaq` ·
