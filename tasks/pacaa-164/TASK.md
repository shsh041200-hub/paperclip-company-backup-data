---
name: "[Autonomy Phase 1] CEO 외부 토큰 5종 부여 — 보드 처리 큐"
---

## 목적

PACAA-161 자율성 Phase 1 — 보드 결정 트레일:
- 2026-05-01 옵션 A 선택 → 4 항목
- 09:02 KST 운영비 envelope 항목 제거 → 3 항목
- 09:15 KST **wake 단순 부여 → 보류 (이벤트 기반 자동 wake 로 대체 검토). terminate 영구 보드 전용. 토큰만 즉시 부여.**

따라서 본 이슈 = **외부 토큰 5종 부여만 보드 처리 큐.**

---

## 보드 액션 체크리스트 (1개로 축소)

### 외부 시스템 서비스계정 / API 토큰 발급

- [ ] **Vercel** API 토큰 (deploy / env vars 읽기) — Backend + CEO 공용
- [ ] **Cloudflare** DNS API 토큰 (TXT/CNAME 추가, 도메인 lock 변경 불가) — Backend 우선
- [ ] **GSC + Naver Search Advisor** 서비스 계정 — sitemap 제출, URL inspection
- [ ] **Plausible** API 토큰 (read-only metrics)
- [ ] **GitHub** PAT (`shsh041200-hub/pkging-platform` repo PR open/merge 권한, settings 변경 불가)

**저장 위치:** `$AGENT_HOME/config/external-tokens.json` (chmod 600, workspace-local) 권장. CEO 가 보드 token 입력 후 chmod 600 자동 처리.

**가드:** 모든 토큰 7-day 회전 가능, scope 최소화, 사용 로그 daily digest 첨부 (PACAA-53 routine 활용).

**Reversibility:** two-way door — 보드가 30초 내 각 서비스에서 revoke 가능.

---

## 별도 처리 (본 이슈 범위 외)

### Wake 권한 — 이벤트 기반 자동 wake 분석으로 전환

보드 코멘트 (PACAA-161 813c9644, 2026-05-01 09:15) 에 따라:

- 단순 자유 wake 권한 = **영구 보류** (runaway / 통제 약화 / audit 위험).
- 대신 **이벤트 기반 자동 wake** 시스템 분석 + 보드 사인오프 후 구현.
- 분석 산출물: 별도 child issue 로 분리 (CEO 본인 작업).

### Term
