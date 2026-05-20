---
name: "[PACAA-924 H] AGENTS.md governance 블록 5개 → packlinx-governance skill reference"
assignee: "cto"
---

PACAA-924 H 마무리.

**완료 (CEO)**:
- packlinx-governance skill 생성 (id `77c57f25`, slug `packlinx-governance`)
- 5개 sub-agent (CTO/Backend/FE/CMO/Legal Counsel) `desiredSkills`에 추가 완료
  - 검증: agent `adapterConfig.paperclipSkillSync.desiredSkills` 에 `company/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance` 포함

**CTO 작업**:
1. 5개 AGENTS.md (CTO/Backend/FE/CMO/Legal Counsel) 에서 다음 블록 제거:
   - HARD RULE board-facing interactions
   - Escalation Protocol (PACAA-143)
   - No `in_review` sleep (PACAA-277)
2. 동일 위치에 1~2줄 reference 삽입:
   `> 거버넌스 하드룰 — board-comms 금지 / Escalation Protocol / in_review sleep 금지 — `packlinx-governance` skill 통합. 매 heartbeat 시작 시 해당 skill 먼저 읽고 따른다.`
3. dedup 검증: `HARD RULE` / 직접 `request_confirmation` 금지 문구 grep = 0 hit (reference 줄 제외)

**검증**:
- `grep -l 'HARD RULE' /home/rlatjsgur/.paperclip/instances/default/companies/d5e183da-*/agents/*/instructions/AGENTS.md` → 빈 결과
- 각 AGENTS.md 에서 packlinx-governance 참조 1회 이상

**Skill MD 경로**: `/home/rlatjsgur/.paperclip/instances/default/skills/d5e183da-c58f-4124-8075-493330dce4c4/packlinx-governance/SKILL.md`
