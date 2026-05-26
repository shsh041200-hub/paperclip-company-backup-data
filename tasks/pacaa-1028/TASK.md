---
name: "[PACAA-896 후속] /compare/* GSC 수동 재제출 + CTO 추가 조치 검토"
assignee: "cto"
---

## 배경

PACAA-896 soak 2주차 확인 결과: site:packlinx.com/compare = **0건** (2026-05-27, D+14 미색인).

Fix 적용(2026-05-13, commit 183da11) 후 2주 경과했으나 Google이 /compare/* 페이지를 미색인.

## 요청 조치

1. **GSC 수동 재제출**: Google Search Console에서 다음 URL 수동 색인 요청
   - https://packlinx.com/compare/박스제조업체-포장지제조업체
   - https://packlinx.com/compare/라벨인쇄업체-스티커제조업체
   (GSC_SERVICE_ACCOUNT_JSON 미설정으로 CMO 직접 제출 불가)

2. **추가 조치 검토**: 2주 후에도 미색인인 원인 분석
   - Crawl budget 이슈 여부
   - Internal linking 강화 필요 여부
   - 페이지 품질/thin content 이슈 여부

## 완료 기준

- GSC 수동 재제출 완료 기록
- 추가 조치 권고사항 또는 기다림 지속 판단 기록
