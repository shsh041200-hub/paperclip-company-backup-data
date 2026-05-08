---
name: "[Surface 2 시정] vendor enrichment PIPA §15 출처 분기 확정 + §39-3 채널 정비"
assignee: "backend-engineer"
---

## 컨텍스트

[PACAA-241](/PACAA/issues/PACAA-241) Surface 2 회고 자문 결과(risk 조건부 `중간`) 후속 시정.

자문 원문: 본 parent issue 댓글 `Surface 2 — vendor 데이터 enrichment` 참조.

## 핵심 작업: enrichment 출처 분기 확정 + 분기별 조치

### Step 1 — 출처 분기 확정 (Backend Engineer + CTO)
[PACAA-78](/PACAA/issues/PACAA-78) 에서 사용한 vendor 전화·주소 enrichment 의 데이터 source 가 아래 어디에 해당하는지 확정 후 댓글로 명시:

- **분기 A** — vendor 본인 self-submission (가입 폼 입력)
- **분기 B** — 공시 사이트 스크래핑 (사업자등록정보 공개시스템 / 통신판매업 공시 / 국세청 API)
- **분기 C** — 제3자 데이터 브로커 / 유료 enrichment API

### Step 2 — 분기별 조치

**분기 A 인 경우** (risk 낮음)
- vendor 가입·온보딩 폼에 PIPA §15 4항목 (수집항목 / 목적 / 보유기간 / 거부권+거부 시 불이익) 모두 표시되는지 확인. 없으면 추가.

**분기 B 인 경우** (risk 중간)
- 개인사업자 vs 법인사업자 분리. 개인사업자의 자택 겸용 주소·휴대전화 노출 시 vendor 본인 확인 후 공개 처리 (default 비공개).
- vendor 페이지 하단에 "본 정보는 공시·공개정보 기반이며, 정정·삭제 요청은 [채널] 로 문의" 안내 추가.
- 개인정보 처리방침에 "공시정보 수집·이용 — PIPA §15 1항 6호 정당한 이익" 항목 추가.

**분기 C 인 경우** (risk 높음)
- 브로커 계약서·정보제공 동의 증빙 확보. 미확인 데이터는 사용 중지 + 삭제.

### Step 3 — PIPA §39-3 정정·삭제·처리정지 채널 (분기 무관 공통)
- vendor 페이지 / 처리방침 / 푸터에서 정정·삭제·처리정지 요청 채널이 명확히 노출되는지 확인. 없으면 DPO 이메일 또는 고객센터 폼 연결.

## Acceptance

- [ ] 출처 분기 (A/B/C) 댓글로 확정
- [ ] 분기별 조치 이행
- [ ] PIPA §39-3 채널 노출 확인
- [ ] vendor 페이지 표시 항목이 통신판매업법 §13 의무 항목
