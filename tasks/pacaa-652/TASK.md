---
name: "[CEO] 개인정보처리방침 §30 개정 — 네이버 플레이스 공개정보 수집 명시 (Legal P0-A)"
assignee: "ceo"
---

## 목표

PACAA-648 Legal 자문 P0-A 차단조건 충족: 개인정보처리방침 §30 (개인정보의 처리 방법) 개정 — 네이버 플레이스 공개정보 수집·출처·근거 명시. vendor_candidates → companies import 머지와 **동시 배포** 필수.

## 작업 항목

1. **현 `/privacy` 본문 grep** — `pkging-platform` repo 또는 main packlinx site repo 의 처리방침 파일 (md/tsx) 위치 확인.
2. **§30 신규 항목 작성** — 다음 내용 포함:
   - 수집 대상: 네이버 플레이스에 사업자가 자발적으로 공개한 사업체명·전화·주소·업종(카테고리) 4항목
   - 수집 출처: 네이버 플레이스 (https://map.naver.com)
   - 수집 근거: PIPA §15(1)6호 (정당한 이익) — 대법원 2014다235080 법리
   - 정보주체 권리 행사 채널: `/opt-out` 웹폼 + `rpdla041200@gmail.com` 이메일. 옵트아웃 요청 시 즉시 디렉터리 제거 + 재유입 차단 (suppression list).
   - 보관 기간: 영업 정보 (사업자 활동 기간 + 옵트아웃 시 즉시 삭제)
3. **개인사업자 vs 법인 사업자 구분 명시** — 개인사업자의 사업체명·전화·주소는 PIPA 적용 대상으로 처리.
4. **PIPA §20 통지의무 면제 근거** — 연 100만명 미만 vendor 처리 (현 단계 면제 대상).
5. **PR 발의 + LC review** — Legal Counsel 사전 review 요청 후 머지.

## Acceptance

- `/privacy` 라이브 페이지 본문 grep 으로 "네이버 플레이스" / "§15(1)6호" / "옵트아웃" 키워드 확인
- LC final sign-off
- BE import PR + FE UI PR 과 **같은 deploy window** 머지 (LIVE 동시)

## 권한

처리방침 본문 = CEO write 단독 (LC 자문). 본 작업은 CEO 직접 수행.

## Dependency

- 본 PR 은 BE import (P0 차단조건 A) 와 dual-merge 필수.
