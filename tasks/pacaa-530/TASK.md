---
name: "[법률 자문] §5-B 통지 의무 — vendor 가 양방향 연락처 미제공 시 적합 채널 (PACAA-529 edge case)"
assignee: "cmo"
---

## 맥락

- 호출 SG: SG-1 (Vendor coverage) — PIPA + 통신판매업 + 표시광고법 trigger
- 호출 issue: [PACAA-529](/PACAA/issues/PACAA-529)
- 모 issue: [PACAA-507](/PACAA/issues/PACAA-507)
- 선행 자문: [PACAA-509](/PACAA/issues/PACAA-509) — LC §5-B 3요건 (사실 / 사유 / 90일 grace) 제시

## 사실관계

2026-05-11T02:00 KST PACAA-515 (Phase B1) 으로 prod `companies` 테이블 20 vendor 가 `is_verified=false` + `verification_revoked_reason=audit_2026Q2_evidence_missing` 박탈.

박탈 사유: §1 검증 evidence 5종 전무 (BRN / 도메인 / 이메일 / 전화 / 양방향 연락).

**Edge case:** 20 vendor 전원 `email=NULL`, `phone=NULL`. 즉 양방향 연락처 미제공이 §1 박탈 사유 자체. (라이브 Supabase 쿼리 확인)

## 사용 가능 채널

| 채널 | 가능 여부 | 도달 검증 |
|---|---|---|
| 이메일 발송 | **불가** (vendor email 미보유) | — |
| SMS / 전화 | **불가** (vendor phone 미보유) | — |
| 대시보드 배너 (vendor 로그인) | **불가** (vendor 대시보드 계정 0건) | — |
| Packlinx 공개 vendor profile page 박탈 banner | 가능 | 게시 시각 server-log |
| 각 vendor 웹사이트 문의폼 manual 제출 (20건) | 가능 | 도달 unverifiable, spam 위험 |
| WHOIS / 사업자등록부 공개 등기 메일 lookup | 가능 (시간 비용) | 도달 unverifiable |

## 구체 질문

1. **§5-B 통지 의무가 vendor 가 양방향 연락처를 자체 제공하지 않은 경우에도 동일하게 적용되는가?** 적용된다면 양자 합의 없는 일방 listing 의 박탈에 대한 합리적 이행 기준은?

2. **Packlinx 공개 vendor profile page 의 박탈 banner 게시 (LC §5-B 3요건 "사실 / 사유 / 90일
