---
name: "[PACAA-118] 185 -NNNN slug strip+redirect 통합 SQL 실행 (Q2 hide_now → strip_all 회귀)"
assignee: "backend-engineer"
---

PACAA-118 ask_user_questions Q2 결정: `hide_now` (CEO 결정 코멘트 654b1d84 참조).

## 작업

### 1. Quality 샘플링 (선행 게이트)

179 stub 중 무작위 20건 sample 하여 vendor name 분류:
- **A. 실제 업체명** — 회사 형태 (주식회사·㈜·…포장·…박스 등) 또는 의미 있는 사업체명
- **B. 가비지** — PACAA-79 류 (지명 `경기도`/`대구광역시`, 블로그 `xxx님의 블로그`, 사이즈 `~50cm`, 브랜드 `3M`/`노브랜드`, 음식점)
- **C. 모호** — 판단 불가 (SNS 핸들 / 1단어 unidentifiable)

### 2. 분기 정책 (CEO 사전 정책)

| garbage 비율 (B) | 액션 |
|---|---|
| ≥ 70% | 179 전체 `is_hidden=true` (redirect 생략) |
| 50–70% | A/C 잔여 strip+redirect (PACAA-121 land 후 SQL 1회 실행), B 만 hide |
| < 50% | 정책 회귀 — 179 모두 strip+redirect (Tier A 6건과 묶어 PACAA-118 본 acceptance 통일 처리) |

중간 비율은 CEO comment 로 escalate; 명백한 ≥70% / <50% 만 자동 진행.

### 3. 실행

- 분기 결정 후: SQL migration draft → CTO sign-off (PACAA-120 와 묶음) → execute on staging → companies SELECT 검증 → prod
- hidden 처리 분: `is_hidden=true, hidden_reason='pacaa118_stub_phone_address_null'`
- redirect 처리 분: PACAA-121 land 대기 → slug_redirects 1회 INSERT

### 4. Acceptance

- [ ] 샘플링 보고서 코멘트 (분포 + 결정)
- [ ] DB: `WHERE slug ~ -[0-9]+$ AND is_hidden=false AND id NOT IN (slug_redirects.from_id)` = 0건
- [ ] PACAA-118 본 이슈에 결과 cross-link

## 의존성
- 샘플링은 **즉시 가능** (PACAA-116 무관).
- redirect 분기 실행은 PA
