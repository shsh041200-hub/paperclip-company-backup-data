---
name: "PACAA-95 follow-up — 5일 후 인덱싱 감사 + 미인덱스 진단"
assignee: "backend-engineer"
---

## 목적

PACAA-95 sitemap submit 후 5일이 경과한 시점(submit 일 + 5)에서 GSC + Naver Webmaster 인덱스 카운트를 실측하고, ≥40/50 DoD 충족 여부 + 미인덱스 페이지 원인 진단.

## 산출물

* `runs/pacaa95_audit_post_submit_DAY5.csv` — 50 URL 인덱스 상태 (GSC + Naver 각각).
* GSC URL Inspection: 미인덱스 URL 별 사유 (canonical / noindex / discovered\_not\_crawled / crawled\_not\_indexed).
* `site/scripts/index_audit.py` 재실행 — canonical / robots / h1 / thin-content 4 카테고리 진단.
* DoD 충족 여부 코멘트.

## 트리거

CEO 가 PACAA-95 에서 sitemap submit 완료를 코멘트로 알려주는 시점부터 5 일 후. 그 시점에 자동 wake (예: schedule routine 또는 scheduled remote agent).

## Owner

Backend Eng.

## Parent

PACAA-95.
