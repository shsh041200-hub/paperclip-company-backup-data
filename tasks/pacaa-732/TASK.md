---
name: "[E6 follow-up] Naver Webmaster 자격증명 통합 — env 변수 정의 + acquisition 가이드"
assignee: "ceo"
---

## 컨텍스트

PACAA-724 인터랙션 `d7b76c53` 보드 응답: **`provide`** (자격증명 제공 — adapterConfig.env로 직접 주입).

따라서 다음 3단계가 남음:

## Deliverable

### 1) 환경변수 이름 canonical 정의

* E6 routine 코드가 읽을 정확한 env var 이름 정의 (예: `NAVER_SEARCHADVISOR_API_KEY`, `NAVER_SEARCHADVISOR_API_SECRET`)
* E6 routine skill / 구현 코드에 박기

### 2) E6 routine 코드 업데이트

* Naver Webmaster `indexing-status` API 호출 통합 (현재 GSC만 동작)
* 자격증명 누락 시 audit log에 `naver_skipped: missing_creds` 기록, GSC만 진행 (kill switch 자동화)

### 3) 보드 인터랙션 (acquisition 가이드)

* env 이름 확정 후 `ask_user_questions` 또는 board UI guide comment
* 내용:
  * Naver Search Advisor 포털 URL (https://searchadvisor.naver.com)
  * 사이트 등록 → API 키 발급 화면 step-list (1-A/1-B 분해, \[\[feedback\_board\_dashboard\_guide\_v2\_first.md]])
  * adapterConfig.env에 입력할 키 이름 정확히 명시
  * 자격증명은 코멘트 금지 — adapterConfig.env로만 (\[\[feedback\_secret\_via\_adapterconfig\_not\_comment.md]])

## Acceptance

* E6 routine 코드에 NAVER\_\* env 이름 grep 가능
* routine 1회 dry-run에서 자격증명 없을 때 `naver_skipped: missing_creds` audit log
* 보드 인터랙션 발의 + step list 완성 (1-A/1-B 분해)
* 자격증명 보드 입력 후 다음 daily run에서 Naver 데이터 추출 확인

## 우선순위 메모

GSC만으로도 keywords.packlinx.com 색인 측정 가능 (PACAA-730 진단 결과). Naver는 보조 채널이라 P2. cap\=2주 안에 완료.
