---
name: "[PACAA-228 child] Supabase Disk IO 완화 보조 — 테이블 prune audit (drop 전 board confirm 필수)"
assignee: "backend-engineer"
---

## 배경

PACAA-228 (parent): Supabase pkging-platform 의 Disk IO Budget 소진 추세. 메인 fix 는 PACAA-230 (Next.js 캐시 활성화). 본 ticket 은 보조 효과 — 사용 안하는 테이블 / 오래된 로그 행 prune 으로 향후 IO 일부 감소 + buffer 효율 개선.

**보드 직접 지시**: "필요한건 절대 삭제하면 안돼 하나하나 다 체크해보면서 줄여" — 따라서 본 ticket 은 **2단계 분리** 진행. 1단계 audit, 2단계 (보드 confirm 받고) 실행.

## 1단계 — Audit only (이 ticket 의 단독 deliverable)

### 산출물 (board comment 로 게시)

모든 public schema 테이블에 대해 다음 표:

| table | row_count | size_total | size_indexes | last_modified | code_refs | 분류 | 비고 |
|---|---|---|---|---|---|---|---|
| companies | ... | ... | ... | ... | N | KEEP | 핵심 |
| ... | ... | ... | ... | ... | ... | KEEP / PRUNE_CANDIDATE / NEEDS_INVESTIGATION | ... |

**code_refs**: pkging-platform 레포 (`~/.paperclip/instances/default/projects/d5e183da-…/f0cad884-…/pkging-platform`) 와 PoC 레포 (`~/.paperclip/instances/default/workspaces/e50c5dc8-…/life/projects/packlinx-web`) 양쪽에서 `from('table_name')` + `'.from("table_name")'` + RPC 함수 내부 참조 grep. 0건 = 후보, 1+ = KEEP.

**분류 기준**:
- `KEEP`: 코드 참조 1+ OR 외래키 inbound 1+ OR Supabase Auth 시스템 테이블
- `PRUNE_CANDIDATE`: 참조 0 + 외래키 0 + 1주 이상 미수정 + 100MB+ 또는 100k+ rows (pruning 가치 있는 크기)
- `NEEDS_INVESTIGATION`: 참조 0 인데 size 작거나 (확신 어려
