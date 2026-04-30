---
name: "PACAA-91 Phase 3 — 유리·금속 + 포장기계 6 키워드 자동 발굴 (Backend)"
assignee: "backend-engineer"
---

## 산출물

유리·금속 용기 카테고리 +3 키워드, 포장기계·자동화 카테고리 +3 키워드. 총 6 키워드 vol≥50 + B2B intent (제작/도매/업체/가격/제조).

PACAA-91 v1.1-final 의 6 [GAP] 슬롯 (G01~G06) 을 채워 50/50 도달.

## 발굴 방법

(b) Backend 자동 발굴 (자격증명 불필요):
1. Naver DataLab API (`/v1/datalab/search`) — 시드 키워드 (`유리병`, `유리용기`, `포장설비`, `자동포장`, `라벨링머신` 등) 의 trend + 연관 검색어 조회
2. Google Trends (pytrends) — 한국 region, 12개월 trend + related queries
3. 후보 추출 → vol≥50 추정 (DataLab 상대치 + 관련 head-term 절대치 보정)
4. 보드 사후 검토용 csv 첨부

## DoD

1. 6 키워드 후보 csv (vol 추정 + 카테고리 + intent)
2. PACAA-82 plan §12 v1.2 패치 — G01~G06 → 실 키워드
3. PACAA-93/94 full unblock 알림

## Owner

Backend Engineer (3177894b). 자격증명/외부 도구 불필요. 보드 사후 검토만 필요.

## 의존성

- 부모: PACAA-91 (v1.1-final 사인오프 완료)
- 영향: PACAA-93 SERP 검증 + PACAA-94 랜딩 빌드 — v1.2 부터 50 키워드 전량 적용
