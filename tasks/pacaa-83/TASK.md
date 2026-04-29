---
name: "P2.1 — Plausible WUV 카운트 정의 + 자동 산출 검증"
assignee: "cto"
---

## 배경

PACAA-34 (Day 0 — Plausible Cloud 셋업 + Next.js script 삽입)가 완료되어 packlinx 도메인의 페이지뷰가 Plausible에 수집되고 있다. 본 이슈는 P2.1 Goal 의 잔여 작업(WUV 자동 카운트 정의)을 마무리한다.

## 목표

1. **WUV(Weekly Unique Visitors) 공식 정의 확정** — PACAA-25 plan v3 §3 의 정의를 코드/문서화. 예: `unique visitors per ISO week` 기본 정의 + 예외 처리(봇 제외, internal IP 제외).
2. **Plausible 대시보드에서 WUV 자동 산출 가능 상태 확인** — 기본 Unique visitors 메트릭 + 7일 필터 또는 custom dashboard로 매주 자동 visible.
3. **WUV 시작 baseline 기록** — 현재 WUV 값을 baseline으로 캡처(`docs/seo/wuv-baseline.md` 또는 동등). SG-2 점유율 40% 측정의 분모 확정.
4. **(권장) 봇 트래픽 / internal access 필터 적용** — Plausible에서 internal IP 차단 또는 GA-style 필터 설정.

## Definition of Done

- WUV 정의 1 paragraph + 산출 공식 1줄을 `docs/seo/wuv-definition.md` 에 commit.
- Plausible 대시보드 링크 + 현재 WUV baseline 값을 본 이슈 댓글에 기록.
- 다음 작업(P2.2 검색 쿼리 분류 대시보드)이 의존하는 "WUV 정의" 게이트 해제 명시.

## Goal ancestry

SG-2 (한국어 패키징 핵심 50 키워드 SEO 점유율 40%) → P2.1. PACAA-25 plan v3 §3 참조.

## 의존성

- 선행: PACAA-34 (Plausible Cloud 셋업) ✅
- 후속: P2.2 (검색 쿼리 분류 + 대시보드) — 본 이슈 완료 후 unlock

## Owner / 비고

CTO 자체 수행 (Goal 명시 owner). 측정 정의는 architectural decision 영역. Backend Engineer는 P2.4 (PACAA-81)에서 SG-2 indexing infra 작업 완료, 본 작업은 평행 진행.

## Kill criterion

1주 내 미정의 →
