---
name: "[Autonomy Phase 1] CEO 외부 토큰 5종 부여 — 보드 처리 큐"
assignee: "ceo"
---

## 목적

**[2026-05-03 SCOPE SHRINK]** 보드 "a" (Option A) 응답에 따라 5종 → **2종 즉시 발급** 으로 축소. Vercel / Cloudflare DNS / GitHub PAT 는 just-in-time (필요 ticket 발생 시점에 별 ask) 로 전환.

PACAA-161 자율성 Phase 1 — 보드 결정 트레일 (2026-05-01 옵션 A → 4 항목 → 3 항목 → 토큰만; 2026-05-03 5종 → 2종).

---

## 보드 액션 — 즉시 발급 2종

### 1. Plausible API 토큰 (read-only)

**언제 필요:** 내일 2026-05-04 PACAA-89 W18 baseline 캡처 시점.

**단계:**
- 1-A. plausible.io 로그인
- 1-B. 우상단 사용자 아이콘 → "Settings" 클릭
- 1-C. 좌측 메뉴에서 **"API Keys"** 클릭 (URL: `plausible.io/settings/api-keys`)
- 1-D. 우상단 **"+ New API Key"** 버튼 클릭
- 1-E. Name: `packlinx-readonly-2026-05`, Permissions: **"Read-only"** 만 체크
- 1-F. **"Continue"** 클릭 → 토큰 노출됨 (한 번만 표시, 닫으면 다시 못 봄)
- 1-G. 토큰 복사 → 본 ticket 코멘트에 붙여넣기 (form: `PLAUSIBLE_API_KEY=plausible_xxxxxxx`)

**검증 신호:** 토큰 입력 후 CEO 가 `curl -H "Authorization: Bearer <token>" https://plausible.io/api/v1/stats/aggregate?site_id=packlinx.com&period=7d&metrics=visitors` 200 응답 확인 후 답글로 ✅ 게시.

### 2. Google Search Console + Naver Search Advisor 서비스 계정

**언제 필요:** 2026-05-05 09:07 KST PACAA-95 audit routine `caf070e6` 자동 fire 시점.

#### 2-A. Google Search Console 서비스 계정
- 2-A-1. https://console.cloud.google.com/ 로그인 (packlinx 도메인 owner
