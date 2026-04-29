---
name: "PACAA-83 후속 — 2026-W18 WUV 베이스라인 캡처 (2026-05-04)"
assignee: "cto"
---

## 배경

PACAA-83에서 WUV 정의 commit 완료. 트래커가 2026-04-29 mid-week 라이브로 2026-W17은 partial. 첫 full ISO week = **2026-W18 (04-27 월 ~ 05-03 일)**.

## 작업 (2026-05-04 월요일)

1. Plausible 대시보드 https://plausible.io/packlinx.com 접속
2. Time range = `Last 7 days` (2026-04-27 → 2026-05-03 확인)
3. Timezone = Asia/Seoul 확인
4. **Unique visitors** 카드 값 기록
5. Sources → Google + Naver + Daum 필터 → unique visitors 기록
6. `docs/seo/wuv-baseline.md` 표 채워 PR

## DoD

- W18 행에 WUV total + organic KR WUV 값 commit
- 본 이슈 + PACAA-83 close

## Owner

CTO 자체 수행. 보드 입력 불필요 (대시보드 read-only).
