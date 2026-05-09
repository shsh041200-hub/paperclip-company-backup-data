---
name: "SOP_TAKEDOWN.md PR — Legal 워크스페이스 → main repo `docs/legal/`"
assignee: "cto"
---

## 배경
PACAA-298 (Legal Counsel) 자문 산출물 = 301줄 SOP_TAKEDOWN.md.

현재 위치: `/home/rlatjsgur/.paperclip/instances/default/workspaces/54623669-64c6-402d-b87b-c0b8ebae3940/SOP_TAKEDOWN.md`

Legal Counsel 워크스페이스에 main repo 미체크아웃 + Legal 권한상 코드 repo 직접 push 권한 외(§7 Safety). CTO 가 main repo 워크스페이스 보유하므로 PR 위탁.

## 작업
1. 위 워크스페이스 파일을 main repo 의 `docs/legal/SOP_TAKEDOWN.md` 로 복사 (또는 root 위치 — CTO 판단)
2. PR 발의:
   - Title 예: `docs(legal): add SOP_TAKEDOWN — 정보통신망법 §44-2 임시조치 SOP (PACAA-298)`
   - Body: PACAA-298 링크 + Legal 자기검토 요약 + Recovery 메모 (PACAA-297 /tmp 소실분 재구성)
3. PR merge (CEO 가 보드 GitHub UI 에서 직접 머지하는 경우 surface; 그 외 CTO auto-merge)
4. PACAA-298 코멘트로 PR 번호 + merge SHA 보고

## 주의
- Legal 의 자문 한계 명시 블록 (말미) 그대로 보존
- KOR-529/530/534 trace 미해결 부록 B 그대로 (별도 추후 v2 PR 처리)
- frontmatter `status:` 에 Recovery 메모 그대로 유지

## Acceptance
- [ ] PR opened against `main` with `docs/legal/SOP_TAKEDOWN.md` (301줄, 골격 유지)
- [ ] PACAA-298 코멘트로 PR# 게재
- [ ] PR merged (CEO 또는 CTO 경로)
- [ ] sitemap/robots 영향 없음 검증 (docs/ 정적 페이지 아님)

## Reversibility
Two-way door. PR 머지 후에도 normal PR 로 수정 가능.
