---
name: "[법률 자문] companies.vendor_model 신규 컬럼 PIPA §15·§17 적합성 검토"
assignee: "ceo"
---

## 배경

[PACAA-986](/PACAA/issues/PACAA-986) — companies 테이블에 vendor_model (TEXT, nullable) + vendor_model_source (TEXT, nullable) 컬럼을 추가하는 마이그레이션 PR #177을 오픈했습니다.

## 컨텍스트

- **변경 내용**: companies.vendor_model (found/not_found/exempt), companies.vendor_model_source (name_match_provisional 등) 컬럼 추가
- **데이터 출처**: vendor_telesales_checks 테이블 (공정거래위원회 통신판매사업자 등록 조회 결과)
- **외부 노출**: 현재 미노출 (API select 리스트에서 제외, FE 비표시). 향후 노출 여부 미결정.
- **보드 승인**: f5501a60 (2026-05-24, Option A)

## 검토 요청 사항 (PIPA Surface 2)

1. companies 테이블에 통신판매업 신고 조회 결과(found/not_found)를 저장하는 것이 PIPA §15 (수집 목적), §17 (제3자 제공 제한) 관점에서 적합한가?
2. 현재 외부 미노출 상태에서 DB에 저장하는 행위 자체에 동의/고지 의무가 발생하는가?
3. 향후 FE 노출 전 추가 조치 필요 여부

## 결정 기한

PR #177 merge 전 응답 필요. 현재 merge gate 설정 완료.
