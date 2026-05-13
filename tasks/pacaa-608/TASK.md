---
name: "[CTO] Daily Board Digest 버그 — pending interactions 미surface"
assignee: "cto"
---

## 배경

오늘 09:00 KST Daily Board Digest (PACAA-607) 가 본문에 "결재 대기 인터랙션 0건" 보고. 라이브 실제 = pending 인터랙션 5704542e (PACAA-168 자격증명 회전) **1건**. 결과: 보드가 19h+ pending P0 보안 항목 미surface 상태.

## 원인

`generate-digest.py` (또는 routine 코드) 의 `escalation_grep` 룰이 코멘트 keyword (`[ESCALATION → CEO]`, `에스컬레이션 → CEO`, `^Blocked.*CEO`) 만 매칭. **kind=ask_user_questions / request_confirmation status=pending 인터랙션은 검색 안 함.**

## 작업

1. `generate-digest.py` (또는 동등 코드) 에 pending interactions count 추가:
   - `GET /api/companies/{cid}/interactions?status=pending` 전수 fetch (또는 in_progress/blocked 이슈 sweep 시 issue-별 interactions GET).
   - body 에 `pending: N` meta-line 추가 (escalation_grep 옆).

2. age-threshold 룰: 
   - pending ≥ 4h → 보드 액션 섹션 강제 surface (idempotency: `digest:{date}:pending:{interactionId}` 로 dedup).

3. 디지스트 본문 형식 갱신:
   - 기존: `escalation_grep: N hit / dormant: M / healthy: K`
   - 신규: `escalation_grep: N hit / dormant: M / healthy: K / pending_interactions: P`

4. SOP `HEARTBEAT.md` Appendix A 동시 업데이트 — "1+ pending = 보드 액션 섹션 강제" 룰 추가.

## Acceptance

- [ ] 라이브 5704542e pending 상태에서 다음 디지스트 fire 시 `pending_interactions: 1` 명시 + 보드 액션 섹션 5704542e 링크.
- [ ] PR + 머지 + 다음 fire (5/14 09:00 KST) 검증.
- [
